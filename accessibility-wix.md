# Categories of Disability
- Visual (Blindness, colorblindness)
- Auditory
- Motor
- Cognitive
- temporary, permanent, situational
- 25% of users can be assumed to have a disability
- Strive to meet WCAG AA to be accessible to widest majority of users.


## Navigation and Pages
- Set the language attribute to allow screen readers to load the proper language module. Settings > Language and Region in Wix, use meta tag in HTML
- Pages should be named using Sentence case for menu purposes in Wix.
- Each page has a Title, which should communicate what your page is and is for, to users coming from google. Set in Main Pages > SEO Basics > Title Tag. Or use meta tag.
- All sites should have an accessibility statement. Make it a page that you can hide from your main menu, and place int the footer.
- Navigation should have good contrast, hover and clicked styles
- To comply with WCAG, you must provide at least two different ways to navigate your site. E. g. search and main menu.
- Form field should have permanently visible lable.
- Form field should have permanently visible submit message.
  
## Colors and Text
Wix themes have 5 colors, each in 5 shades. Number them 1-25. The important ones are:
- 1 Background
- 4 Accent color
- 5 Main Text
- 8 Action
Colors 4, 5, and 8 must have a minimum contrast ratio of 4.5:1 to color 1. Use [WebAIM](https://webaim.org/resources/contrastchecker/) to check

For text, favor sans-serif for body text. It is easier to read. Can use a serif for headings to add sophistocation.  Body text should be no smaller than 16px. Can go down to 14px for secondary text, such as in footer.

## Content and Heading Tags
Each page must have exactly one h1 tag, and each other tag must follow the heirarchy. For example, do not use an h1 and then skip h2 and use 12 h6s. An h3 cannot be above an h2. Each section must contain a heading. You can manipulate which tag is used under SEO and Accessibility > tag. Sighted and unsighted users use headings to navigate and skip though your content without having to read everything.

When writing accessible content, include only one main point as the first (topic) sentence of each paragraph. Breaks between paragraphs help users keep their place and understand the main point. Here are some helpful guides:
- Links must make sense out of context! They must be at the end of a sentence. Describe where the link will take you!
- Sentences should be 15 words on average.
- Name the person rather than the condition (People with Celiac's disease, not "Celiacs")
- Avoid negative conditional contractions ("wouldn't"). They increase cognitive load.
- Avoid hyphenated words when possible. They mess with screen readers.
- Use inclusive language (gender, disability status, etc...).
- Justified text is aligned on the left and right. It is awful and don't do it.
- Don't use unneccessary acronyms. Do not assume everyone knows what it means.

## Alt Text for Images
Alt Text should communicate the intended purpose of the image. Do not describe irrelevant details. Add it in Image Settings > "whats in this image? Tell Google". When text appears in an image, quote that text. Purely decorative images do not need alt text. Wix will automatically tell screen readers to ignore blank alt text images that serve a decorative purpose. Informative images (Email icon for example) should have alt text that describes their function ("email"). Functional image alt text (logo linked to home page) should say what it is and what it does. It will say that it is a link automatically, so do not write "Henry's Bakery Logo, links to homepage", write "Henry's Bakery Logo, Homepage". Complex images should have a concise description in the alt text. Describe the meaning and importance of the information in the graphic in the main text. Can attach an excell file containing the data so that unsighted users can access each data point.  Other dos and donts:
- Keep alt text below 100 words
- Use simple words
- Don't try to use 10 different keywords in alt text. It is annoying, and doest even help with anything.
- Always describe the purpose of the image.

## Alternative media
- Add transcripts for audio and video. 
- Do not autoplay media.
- Avoid unneccessary paralax backgrounds.
- Do not annimate elements that have core functionality

## Zoom
Users should be able to zoom to 200% without any loss of funcionality, according to WCAG. Make sure that pinned elements do not overlap with anything important on zoom. 
