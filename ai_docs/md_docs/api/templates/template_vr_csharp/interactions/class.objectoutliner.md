# ObjectOutliner Component

**Inherits from:** Component


ObjectOutliner provides static methods for rendering outline effects on objects. It can redirect outlines from one object to another and renders all accumulated outlines in a single pass.


## ObjectOutliner Class

---

## static void RenderOutlineForObject ( )

Adds the specified object to the outline render queue.
### Arguments

## static void ResetObjects ( )

Clears all objects from the outline render queue.
## static void RedirectOutlineForNode ( )

Redirects outline rendering from one object to another.
### Arguments

## static void ClearRedirect ( )

Clears all outline redirections.
## static void Render ( )

Renders outlines for all queued objects.
