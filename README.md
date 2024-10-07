  # Bookletic :book:
Create beautiful booklets with ease.

The current version of this library (0.3.0) contains a single function to take in an array of content blocks and order them into a ready to print booklet, bulletin, etc. No need to fight with printer settings or document converters. 

### Example Output

Here is an example of the output generated by the `sig` function (short for a book's signature) with default parameters and some sample content:

![Example1](example/basic.png)

Here is an example with some customization applied:

![Example2](example/fancy.png)

## `sig` Function

The `sig` function is used to create a signature (booklet) layout from provided content. It takes various parameters to automatically configure the layout. 

### Parameters

- `page_margin_binding`: The binding margin for each page in the booklet (space between pages).
- `page_border`: Takes a color space value to draw a border around each page. If set to none no border will be drawn.
- `draft`: A boolean value indicating whether to output an unordered draft or final layout.
- `p-num-layout`: A configuration for page numbering styles, allowing multiple layouts that apply to specified page ranges. Each layout can be provided as a dictonary specifying the following options:
    - `p-num-start`: Starting page number for this layout
    - `p-num-alt-start`: Alternative starting page number (e.g., for chapters)
    - `p-num-pattern`: Pattern for page numbering (e.g., `"1"`, `"i"`, `"a"`, `"A"`)
    - `p-num-placment`: Placement of page numbers (`top` or `bottom`)
    - `p-num-align-horizontal`: Horizontal alignment of page numbers (`left`, `center`, or `right`)
    - `p-num-align-vertical`: Vertical alignment of page numbers (`top`, `horizon`, or `bottom`)
    - `p-num-pad-left`: Extra padding added to the left of the page number
    - `p-num-pad-horizontal`: Horizontal padding for page numbers
    - `p-num-size`: Size of page numbers
    - `p-num-border`: The border color for the page numbers. If set to none no border will be drawn.
    - `p-num-halign-alternate`: A boolean for whether to alternate horizontal alignment between left and right pages.
- `pad_content`: The padding around the page content.
- `contents`: The content to be laid out in the booklet. This should be an array of blocks.

### Usage

To use the `sig` function, simply call it with the desired parameters and provide the content to be laid out in the booklet:

```typst
#set page(flipped: true, paper: "us-letter")
#sig(
  contents: [
    ["Page 1 content"],
    ["Page 2 content"],
    ["Page 3 content"],
    ["Page 4 content"],
  ],
)
```

This will create a signature layout with the provided content, using the default values for the other parameters.

You can customize the layout by passing different values for the various parameters. For example:

```typst
#set page(flipped: true, paper: "us-legal", margin: (top: 1in, bottom: 1in, left: 1in, right: 1in))
#sig(
  page_margin_binding: 0.5in,
  page_border: none,
  draft: true,
  p-num-layout: (
    (
      p-num-start: 1,
      p-num-alt-start: none,
      p-num-pattern: "~ 1 ~", 
      p-num-placment: bottom,
      p-num-align-horizontal: right,
      p-num-align-vertical: horizon,
      p-num-pad-left: -5pt,
      p-num-pad-horizontal: 0pt,
      p-num-size: 16pt,
      p-num-border: rgb("#ff4136"),
      p-num-halign-alternate: false,
    ),
  ),
  pad_content: 10pt,
  contents: (
    ["Page 1 content"],
    ["Page 2 content"],
    ["Page 3 content"],
    ["Page 4 content"],
  ),
)
```

This will create an unordered draft signature layout with US Legal paper size, larger margins, no page borders, page numbers at the bottom right corner with a red border, and more padding around the content.

### Notes
- The `sig` function is currently hardcoded to only handle two-page single-fold signatures. Other more complicated signatures may be supported in the future.
- The `booklet` function is a placeholder for automatically breaking a single content block into pages dynamically. It is not implemented yet but will be added in coming versions.

## Collaboration
I would love to see this package eventually turn into a community effort. So any interest in collaboration is very welcome! You can find the github repository for this library here: [Bookletic Repo](https://github.com/harrellbm/Bookletic). Feel free to file an issue, pull request, or start a discussion. 

## Changlog
#### 0.3.0
- Remove internal dependency on native page function. This allows the user to set the page function separatley with full control over paper type, outer margins and everything else defined by the native page function.
- Add p-num-halign-alternate to page number layout allowing setting page numbers to alternate on facing pages making it possible to place page numbers along the outside or inside edges of facing pages.
- Internal improvments for ordering algorythm algorithm. 
  
#### 0.2.0
- Handle odd number of pages by inserting a blank back cover
- Implements page number layouts to allow defining different page numbers for different page ranges.
- Add various other page number options

#### 0.1.0
Initial Commit
