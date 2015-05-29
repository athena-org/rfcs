- Feature Name: restructure_phosphorus_widgets_into_templates
- Affected Projects: Phosphorus, Any Phosphorus Users
- Start Date: 2015-05-27
- RFC PR: [athena-org/rfcs#3](https://github.com/athena-org/rfcs/pull/3)

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
let template = Layout::new()
    .with_element(Text::new().with_text("Hello!"))
    .with_element(Controller::<MyController>::new()
        .with_binding("MainController")
        .with_element(Text::new().bind(c => c.text_value))
    )
);


// # Code that requires gfx templates:

// Load the elements into a GUI
let gui = gui::new(&mut gfx_factory, template);

// Bind the controllers to their names
let controller = MyController { text_value: "Hello World!" };
gui.bind_controller("MainController", &mut controller);

// Display the Gui
gui.draw(&mut gfx_stream);
```

# Drawbacks

This system is more complex to implement that the previous static widgets system.

# Alternatives

Templating and controllers could be kept in a separate crate from Phosphorus.

# Unresolved questions

The specifics on the API on templates still is mostly undecided.
