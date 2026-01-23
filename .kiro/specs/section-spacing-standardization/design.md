# Design Document

## Overview

The current website has inconsistent spacing between the main sections (Listen, Live, Merch, and Booking) due to different CSS approaches and manual spacing elements. This design establishes a unified section spacing system that creates visual consistency while maintaining the existing design aesthetic.

## Architecture

### Current State Analysis

The existing sections use different spacing approaches:

1. **Listen Section**: Uses `margin-bottom: 3.6rem` from `.section-intro` class
2. **Live Section**: Has manual spacing with `<div class="col-twelve resume-header"></div>` and uses `#resume` styles with `padding-top: 12rem; padding-bottom: 12rem`
3. **Merch Section**: Uses `#services` styles with `padding-top: 12rem; padding-bottom: 12rem` but has manual spacing div
4. **Booking Section**: Uses `#contact` styles with `padding-top: 12rem; padding-bottom: 7.2rem` and has manual spacing div

### Proposed Solution

Create a standardized section spacing system using CSS custom properties (CSS variables) and consistent padding classes that can be applied to all main sections.

## Components and Interfaces

### CSS Custom Properties

```css
:root {
  --section-padding-top: 8rem;
  --section-padding-bottom: 8rem;
  --section-padding-top-mobile: 6rem;
  --section-padding-bottom-mobile: 6rem;
}
```

### Section Spacing Classes

```css
.main-section {
  padding-top: var(--section-padding-top);
  padding-bottom: var(--section-padding-bottom);
}

@media only screen and (max-width: 768px) {
  .main-section {
    padding-top: var(--section-padding-top-mobile);
    padding-bottom: var(--section-padding-bottom-mobile);
  }
}
```

### Section-Specific Overrides

Some sections may need slight adjustments while maintaining the overall consistency:

```css
.main-section.intro-section {
  padding-top: 0; /* Intro section starts at top */
}

.main-section.footer-adjacent {
  padding-bottom: calc(var(--section-padding-bottom) * 0.75); /* Slightly less padding before footer */
}
```

## Data Models

### HTML Structure Changes

Each main section will be updated to use the standardized class:

```html
<section id="listen" class="main-section">
  <!-- existing content -->
</section>

<section id="live" class="main-section grey-section">
  <!-- existing content -->
</section>

<section id="merch" class="main-section">
  <!-- existing content -->
</section>

<section id="booking" class="main-section footer-adjacent">
  <!-- existing content -->
</section>
```

### Removal of Manual Spacing Elements

Remove manual spacing divs like:
```html
<div class="col-twelve resume-header"></div><!-- add padding before next section -->
```

## Error Handling

### Fallback Values

Provide fallback values for older browsers that don't support CSS custom properties:

```css
.main-section {
  padding-top: 8rem; /* fallback */
  padding-top: var(--section-padding-top);
  padding-bottom: 8rem; /* fallback */
  padding-bottom: var(--section-padding-bottom);
}
```

### Responsive Considerations

Ensure spacing scales appropriately across all breakpoints:
- Desktop: 8rem top/bottom padding
- Tablet: 6rem top/bottom padding  
- Mobile: 6rem top/bottom padding

## Testing Strategy

### Visual Regression Testing

1. **Before/After Screenshots**: Capture screenshots of the full page at different breakpoints
2. **Section Spacing Measurements**: Measure pixel distances between sections
3. **Cross-Browser Testing**: Test on Chrome, Firefox, Safari, and Edge

### Responsive Testing

1. **Breakpoint Testing**: Test at 1200px, 768px, 600px, and 400px widths
2. **Device Testing**: Test on actual mobile devices and tablets
3. **Orientation Testing**: Test both portrait and landscape orientations

### Code Quality Testing

1. **CSS Validation**: Validate CSS syntax and properties
2. **Performance Testing**: Ensure no performance regression
3. **Accessibility Testing**: Verify spacing doesn't affect accessibility

### Implementation Approach

1. **Add CSS Variables**: Define spacing variables in the existing CSS structure
2. **Create Section Class**: Add the `.main-section` class with standardized padding
3. **Update HTML**: Apply the class to each main section
4. **Remove Manual Spacing**: Clean up manual spacing elements
5. **Test and Refine**: Adjust values based on visual testing

This approach maintains backward compatibility while providing a clean, maintainable solution for consistent section spacing.