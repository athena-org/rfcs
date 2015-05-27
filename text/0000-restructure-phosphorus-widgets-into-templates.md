- Feature Name: restructure_phosphorus_widgets_into_templates
- Affected Projects: Phosphorus, Any Phosphorus Users
- Start Date: 2015-05-27
- RFC PR: (leave this empty)

# Summary

Replace the current widgets system in phosphorus with a template-based system.
This RPC is intentionally loosely defined as the API's far from stabilizing.

# Motivation

The current widget system works for static UIs but it quickly becomes unmanageable for UIs that have to change depending on user input. This problem already has surfaced in *athena_editor*.

# Detailed design

- Remove the `root` parameter in `Gui::new()` and the `root`, `root_mut` and `get_root` property accessors.
- Remove the current structure of assembling widgets with builders.
- Replace the widget structure with a template structure.
- Make Gui render an actual image using the template and controllers, updating as needed.

The following is a sample piece of code that shows how the Phosphorus API should be used after these changes:

```Rust
// # Code that does not require any gfx templates:

struct MyController {
    pub text_value: String
}

// Set up a view template
let template = template::new()
    .with_element(template::new_text().with_text("Hello!"))
    .with_element(template::new_controller<MyController>("MainController")
        .with_element(template::new_text().for(c => c.text_value))
    )
);


// # Code that requires gfx templates:

// Load the elements into a Gui
let gui = gui::new(&mut gfx_stream, template);

// Set the actual controller data
let controller = MyController { text_value: "Hello World!" };
gui.set_controller("MainController", controller);

// Display the Gui
gui.draw(&mut gfx_stream);
```

`set_controller` performs runtime dynamic casting using `std::any` to pass the data to the actual controller.

# Drawbacks

This system is vastly more complex to implement that the previous static widgets system.

# Alternatives

Templating and controllers could be kept in a separate crate from Phosphorus.

# Unresolved questions

The specifics on the API on templates still is mostly undecided.
