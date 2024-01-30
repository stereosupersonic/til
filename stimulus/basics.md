# Stimuls https://stimulus.hotwired.dev/

## generate a new controller

```
rails g stimulus myname
```


## add class when clicking

1. new stimulus controller

```
rails g stimulus loader
```

2. add code to stimulus controller


```
import { Controller } from "@hotwired/stimulus"

// Connects to data-controller="loader"
export default class extends Controller {
  disableButton(event) {
    this.element.classList.add("disabled")
  }
}
```

3. add trigger to gui (set controler and action)

```
= link_to "Clear", box_path(box.namespace), data: { "turbo-method": :delete, "turbo-confirm": "Are you sure?", controller: "loader", action: "loader#disableButton" }, class: "btn btn-danger btn-sm"

# controller: "loader", action: "loader#disableButton"

```
