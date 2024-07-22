# Show control on hover

A simple way to show a control when users hover over another one. 

https://github.com/user-attachments/assets/d1f94cd4-663d-40ef-be09-e68af87b84dd

# Version 
Current version - Initial 1.0

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Global Script Setup
1. Create a Global Script called "ShowOnHover"
2. Add the input parameters below to the global script
   1. HoveredElementClass
   2. RevealedElementClass
3. Drag a JavaScript action into the script
4. Add the Javascript below into the JavaScript code property
```javascript
/* Stadium Script v1.0 https://github.com/stadium-software/show-control-on-hover */
let scope = this;
let hoverbutton = document.querySelector("." + ~.Parameters.Input.HoveredElementClass);
let hiddenEl = document.querySelector("." + ~.Parameters.Input.RevealedElementClass);
hoverbutton.addEventListener("mouseover", showEl);
hoverbutton.addEventListener("mouseout", hideEl);
function showEl() {
    setDMValues(hiddenEl, "Visible", true);
}
function hideEl() {
    setDMValues(hiddenEl, "Visible", false);
}
let getObjectName = (obj) => {
    let objname = obj.id.replace("-container", "");
    do {
        let arrNameParts = objname.split(/_(.*)/s);
        objname = arrNameParts[1];
    } while ((objname.match(/_/g) || []).length > 0 && !scope[`${objname}Classes`]);
    return objname;
};
function setDMValues(ob, property, value) {
    let obname = getObjectName(ob);
    scope[`${obname}${property}`] = value;
}
```

## Page Setup
1. Drag a Control to the page that you would like users to hover
2. Add a unique classname to the hoverable control (e.g. hovered-element)
3. Drag a Control to the page that will be shown when the element above is hovered
4. Add a unique classname to the showing control (e.g. hidden-container)
5. Set the "Visible" property of the showing control to 'false'

## Page.Load Setup
1. Drag the Global Script called "ShowOnHover" into the Page.Load event handler
2. Provide the two classes that uniquely identify the two page elements as input parameters to the global script
   1. HoveredElementClass: the class of the element usesr can hover (e.g. hovered-element)
   2. RevealedElementClass: the class that the hover action will reveal (e.g. hidden-container)

## Some CSS suggestions
The CSS below can optionally be used to style the two elements by pasting the CSS into the application Sylesheet

```css
.hovered-element {
	height: 26px;
	width: 26px;
	background-image: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxZW0iIGhlaWdodD0iMWVtIiB2aWV3Qm94PSIwIDAgMjQgMjQiPjxwYXRoIGZpbGw9IiNkYjc2NzYiIGQ9Ik0xMS45NSAxOHEuNTI1IDAgLjg4OC0uMzYzdC4zNjItLjg4N3QtLjM2Mi0uODg4dC0uODg4LS4zNjJ0LS44ODcuMzYzdC0uMzYzLjg4N3QuMzYzLjg4OHQuODg3LjM2Mm0tLjktMy44NWgxLjg1cTAtLjgyNS4xODgtMS4zdDEuMDYyLTEuM3EuNjUtLjY1IDEuMDI1LTEuMjM4VDE1LjU1IDguOXEwLTEuNC0xLjAyNS0yLjE1VDEyLjEgNnEtMS40MjUgMC0yLjMxMi43NVQ4LjU1IDguNTVsMS42NS42NXEuMTI1LS40NS41NjMtLjk3NVQxMi4xIDcuN3EuOCAwIDEuMi40Mzh0LjQuOTYycTAgLjUtLjMuOTM4dC0uNzUuODEycS0xLjEuOTc1LTEuMzUgMS40NzV0LS4yNSAxLjgyNU0xMiAyMnEtMi4wNzUgMC0zLjktLjc4N3QtMy4xNzUtMi4xMzhUMi43ODggMTUuOVQyIDEydC43ODgtMy45dDIuMTM3LTMuMTc1VDguMSAyLjc4OFQxMiAydDMuOS43ODh0My4xNzUgMi4xMzdUMjEuMjEzIDguMVQyMiAxMnQtLjc4OCAzLjl0LTIuMTM3IDMuMTc1dC0zLjE3NSAyLjEzOFQxMiAyMiIvPjwvc3ZnPg==');
	background-repeat: no-repeat;
	background-size: 26px;
}
.hidden-container {
	position: absolute;
	padding: 12px;
	border: 1px solid #ccc;
	border-radius: 6px;
	box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
	.control-container {
		margin-top: 0;
	}
}
```

## CSS Upgrading
To upgrade the CSS in this module, follow the [steps outlined in this repo](https://github.com/stadium-software/samples-upgrading)
