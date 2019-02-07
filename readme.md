## &lt;actindo-wizard&gt;

`<actindo-wizard>` implements a generic component to create multi step wizards

## Examples

### basic usage

```
<dom-module id="your-element">
    <template>
         <actindo-wizard on-finished="_onwizardFinished">
             <actindo-wizard-step label="Select type">
                  <your-type-select></your-type-select>
             </actindo-wizard-step>
             <actindo-wizard-step label="Configure source">
                 <your-source-configure></your-source-configure>
             </actindo-wizard-step>
             <actindo-wizard-step label="select data">
                 <your-select-data></your-select-data>
             </actindo-wizard-step>
             <actindo-wizard-step label="Confirm import">
                 <your-confirm-import></your-confirm-import>
             </actindo-wizard-step>
         </actindo-wizard>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            _onwizardFinished(e) {
                let states = e.detail.states;
                // do something with the data in the states
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```

### full example

```
<dom-module id="your-element">
    <template>
         <actindo-wizard 
                 id="wizard"
                 on-finished="_onWizardFinished"
                 disable-continue="[[_isContinueDisabled()]]"
                 disable-cancel="[[_isCancelDisabled()]]"
                 current-step="{{currentStep}}"
                 back-label="Go Back"
                 cancel-label="Abort"
                 continue-label="Next"
                 finish-label="Finish"
                 step-label="Stage"
                 ok-label="Understood"
                 confirm-clear-states-message="This data is lost if you go back:"
                 ask-before-clear-state
                 open>
             <actindo-wizard-step label="Select type">
                  <your-type-select></your-type-select>
             </actindo-wizard-step>
             <actindo-wizard-step 
                     label="Configure source" 
                     on-leave="_onSourceConfigurationLeave"
                     depends-on-previous-step>
                 <your-source-configure></your-source-configure>
             </actindo-wizard-step>
             <actindo-wizard-step 
                     label="select data" 
                     on-enter="_onEnterSelectData"
                     depends-on-previous-step>
                 <your-select-data></your-select-data>
             </actindo-wizard-step>
             <actindo-wizard-step 
                     label="Confirm import" 
                     depends-on-previous-step>
                 <your-confirm-import></your-confirm-import>
             </actindo-wizard-step>
         </actindo-wizard>
    </template>
    
    <script>
        class YourElement extends Polymer.Element {
            static get is() { return 'your-element'; }
            
            static get properties() {
                return {
                    // contains the current step through databinding
                    currentStep: {
                        type: Number
                    },
                };
            }

            connectedCallback() {
                super.connectedCallback();

                let wizard = this.$.wizard;
                wizard.
            }
            
            _onWizardFinished(e) {
                let states = e.detail.states;
                // do something with the data in the states
                // at this stage, the wizard is already closed
            }

            _onEnterSelectData() {
                // called when the user enters the step. use this to load data or perform other step up
                let previousStepData = this.$.wizard.getState(this.currentStep - 1); // this may be of interest
            }

            _onSourceConfigurationLeave(e) {
                // called when the user leaves that step
                // you may cancel this to prevent the user from leaving step (i.e. because the step wasn't finalized)
                e.preventDefault();
            }

            /**
             * @returns {Boolean}
             */
            _isCancelDisabled() {
                // callback function to control the disabled state of the cancel button.
                // may be useful to prevent the user from leaving in a mission critical state
            }

            /**
             * @returns {Boolean}
             */
            _isContinueDisabled() {
                // callback function to control the disabled state of the continue button
            }
        }
        
        customElements.define(YourElement.is, YourElement); 
    </script>
</dom-module>
```
