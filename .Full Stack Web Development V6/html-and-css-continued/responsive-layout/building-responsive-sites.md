# Lesson: Building Responsive Sites

## Notes

### Using Server-Side Detection for Redirection

- Every time your web browser opens a web page, it sends information to the server called a "request", including a series of "headers" which carry information about the client browser, the requested page, the server, and more. It is possible for web servers to check the requesting device's headers information, and send back files specific to the type of device, however, this requires building a separate website for each type of device you wish to accommodate.

### Creating Responsive Sites with CSS

- The other solution is to use Cascading Style Sheets. Instead of a server detecting the type of device, every user receives the same content, and the provided CSS tells the user's browser how to style that rendered page. The ideal approach for a well designed, responsive website relies on a combination of:
  - CSS media queries
  - Responsive layout, text, and media element styling
  - Responding to the viewport size
- Together they create "responsive sites".

#### Desktop-Down Design

- One approach to responsive design is called _Desktop-down_, where a site is first designed for desktop devices, then modified layouts are developed for tablet and mobile devices.
- Desktop-down design often means that, by default, elements on the page are the width and height they should be for a larger screen. When a smaller screen size is detected, the default styling will be overridden and replaced with the rules for tablet or mobile styling.

#### Mobile-First Design

- Going in the opposite direction is the _mobile-up_ or _mobile-first_ approach, designing for small screen sizes first. One benefit to this approach is that it ensures users have a great experience on mobile, as there is no chance it will end up being a second thought during design.
- Mobile-first design means that, by default, elements on the page are positioned and sized for small screens, then overridden if a larger screen is detected.

#### Graceful Degradation

- Graceful degradation is the practice of designing a web page for modern browsers, but providing "fall back" versions, alternative designs that have less features, but still provide a good experience. Fully embracing graceful degradation may mean designing your website to work even without JavaScript or CSS, using the older, most compliant HTML.

#### Progressive Enhancement

- Progressive enhancement means first designing your website to function at its most basic, then upscaling the functionality if the user's browser can handle it.
