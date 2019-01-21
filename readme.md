## &lt;actindo-wizzard&gt;

`<actindo-wizzard>` implements a generic component to create multi step wizzards

## Examples

### basic usage

```
<dom-module id="your-element">
    <template>
         <actindo-wizzard id="wizzard" on-finished="_onWizzardFinished">
             <actindo-wizzard-step label="Select type">
                  <your-type-select></your-type-select>
             </actindo-wizzard-step>
             <actindo-wizzard-step label="Configure source" depends-on-previous-step >
                 <your-source-configure></your-source-configure>
             </actindo-wizzard-step>
             <actindo-wizzard-step label="select data">
                 <your-select-data></your-select-data>
             </actindo-wizzard-step>
             <actindo-wizzard-step label="Confirm import" depends-on-previous-step>
                 <your-confirm-import></your-confirm-import>
             </actindo-wizzard-step>
         </actindo-wizzard>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            static get properties() {
                return {};
            }
            
            _onWizzardFinished(e) {
                let states = e.detail.states;
                // do something with the data in the states
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```
