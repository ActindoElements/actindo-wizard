## &lt;actindo-wizard&gt;

`<actindo-wizard>` implements a generic component to create multi step wizards

## Examples

### basic usage

```
<dom-module id="your-element">
    <template>
         <actindo-wizard id="wizard" on-finished="_onwizardFinished">
             <actindo-wizard-step label="Select type">
                  <your-type-select></your-type-select>
             </actindo-wizard-step>
             <actindo-wizard-step label="Configure source" depends-on-previous-step >
                 <your-source-configure></your-source-configure>
             </actindo-wizard-step>
             <actindo-wizard-step label="select data">
                 <your-select-data></your-select-data>
             </actindo-wizard-step>
             <actindo-wizard-step label="Confirm import" depends-on-previous-step>
                 <your-confirm-import></your-confirm-import>
             </actindo-wizard-step>
         </actindo-wizard>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            static get properties() {
                return {};
            }
            
            _onwizardFinished(e) {
                let states = e.detail.states;
                // do something with the data in the states
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```
