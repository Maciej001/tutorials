#jQuery by Craig Buckler

## Basics

`$('p').css({"color": "red", "font-style" : "italic"});`  - change css property
`$("h1").css("color", "blue").text("Hello");`

## Selectors

`p + p`  - find paragraph that has before sibling paragraph, so if you have 3 paragraphs 
only the 2nd and 3rd will be selected. First paragraph does not have any prev paragraphs

`p:first-child` - paragraph that is the first paragraph of it's container

!!!Important - wherever possible use ID selectors and not class selectors. When you use
class selector it searches the whole DOM on the page.
