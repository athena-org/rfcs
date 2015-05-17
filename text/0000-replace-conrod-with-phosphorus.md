- Feature Name: replace_conrod_with_phosphorus
- Affected Projects: Zeus, Phosphorus
- Start Date: 2015-05-01
- RFC PR: (leave this empty)

# Summary

Replace the current use of the Conrod UI library in zeus with our own Phosphorus UI library. Phosphorus currently does not have the functionality to render the widgets needed for Zeus, so these should be developed.

# Motivation

This was the original goal but time constraints prevented it from being done in the first place. Phosphorus is also supposed to be the UI used for both the editor and for games created with Athena, so it being used would improve uniformity. Phosphorus as well is designed around data binding and markup files, which should work better for large applications than Conrod does.

As well, Conrod is built around and heavily uses the Piston engine for rendering. Keeping the Conrod dependency for Zeus and Athena Editor would mean that the Athena game engine depends on the Piston game engine.

# Detailed design

As mentioned, Phosphorus lacks certain features for it to be used in Zeus, these should be implemented first. The following features have to be added to Phosphorus for it to be useable:

- [x] Implement text rendering on widgets that include text
- [ ] Add button widgets with click callbacks

After those are done, the crate *zeusgui* should be adjusted to use Phosphorus instead of Conrod.

# Drawbacks

Implementing our own UI library is not an easy task. It takes a lot more work than using an existing one.

At this point, markup based UI will not yet be available in Phosphorus, which means we'll have to adjust the frontend again once that becomes available.

# Alternatives

Given the situation, continuing to use Conrod does not seem like a decent alternative, but it could work just a bit longer if Phosphorus isn't an option yet in the short term.

There are options to make bindings for GUI libraries that have a C interface but those will not be as nice to use as a pure Rust one will be.

# Unresolved questions

Will an alternative choice for GUI library still allow us to render a scene as a UI widget, as this is the basis around the engine's planned rendering pipeline. It is certain Phosphorus will since it's from the base built around what we need.
