# Selectable Base Class

The Selectable Class is the base class for all the interaction components and it handles the items that are in common.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Interactible__ | This determines if this component will accept input.  When it is set to false interaction is disabled and the transition state will be set to the disabled state. |
|__Transition__ |Within a selectable component there are several [Transition Options](script-SelectableTransition) depending on what state the selectable is currently in. The different states are: normal, highlighted, pressed and disabled. |
|__Navigation__ |There are also a number of [Navigation Options](script-SelectableNavigation) to control how keyboard navigation of the controls is implemented.  |

