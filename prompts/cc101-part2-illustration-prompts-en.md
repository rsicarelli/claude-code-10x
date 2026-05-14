# CC-101 Part 2 — Illustration Prompts for Gemini Image Generation (English)

Style guide for all images: flat design infographic style, clean lines, vibrant but not neon colors, white or very light gray background. All LEGO bricks must look like classic LEGO 2x4 bricks: flat, wide, and low-profile. Each brick should be approximately 4 times wider than it is tall. Think of them as flat rectangular plates with small round studs on top, NOT cubes or tall blocks. The proportions should match a real LEGO brick lying flat on a table. No photorealism, no 3D rendering, minimal shadows, clear readable labels in English. Consistent color palette: blue for English, orange for Portuguese, green for correct/selected, red for wrong/danger, gray for neutral.

---

## 0. What is a token: text becomes pieces

Horizontal illustration read left to right, showing the transformation of text into tokens. All text in English.

On the left side, a sentence written in plain text as if typed on a screen: "I love chocolate cake". The text is in clean, black font, no decoration.

In the center, a wide arrow pointing right with the word "tokenization" written inside the arrow.

On the right side, the same sentence broken down into individual LEGO bricks arranged in a horizontal row. Each brick shows two pieces of information: the text fragment written on the top face of the brick, and an integer number (token ID) written on the front face of the brick. The bricks have different sizes depending on the fragment:

- Large brick (yellow): "I" / ID: 40
- Large brick (blue): " love" / ID: 3021
- Large brick (green): " chocolate" / ID: 28401
- Large brick (red): " cake" / ID: 11884

Below the row of bricks, the text: "Computers don't understand text. They understand numbers."

Below that, a smaller second line showing granularity variation: the word "tokenization" alone, broken into 4 small bricks: "token" / "iza" / "tion" — with an annotation: "One word can become multiple pieces."

Flat infographic style, white background, LEGO bricks with visible studs on top. Token IDs are invented but plausible numbers (3-5 digits). No arrows besides the central transformation arrow. No text in any other language.

---

## 1. Tokenization: English vs Portuguese

Side-by-side infographic comparing English and Portuguese tokenization. All text in English.

IMPORTANT: All LEGO bricks must be flat and horizontal, like classic 2x4 LEGO bricks seen from the front. Each brick is WIDE and SHORT (roughly 4x wider than tall). They are laid side by side in a single horizontal row, like tiles on a floor. NOT vertical, NOT tall columns.

Left panel with a blue header labeled "English": the full sentence "Have a great day!" printed above. Below it, a single horizontal row of 5 flat wide bricks touching side by side. Each brick is the same height but varies in width proportional to the word length. Colors: blue "Have", green "a" (narrower), yellow "great", teal "day", gray "!". Below the row: "5 tokens".

Right panel with an orange header labeled "Portuguese": the full sentence "Tenha um ótimo dia!" printed above. Below it, a single horizontal row of 8 flat wide bricks touching side by side. These bricks are noticeably NARROWER than the English ones because the same content is split into more pieces. Colors vary. Labels: "Ten", "ha", "um", "ó", "t", "imo", "dia", "!". The bricks for "ó" and "t" are the narrowest of all. Below the row: "8 tokens".

Between the two panels, centered text: "+60% more pieces to say the same thing".

Flat infographic style, white background, no arrows, no flow lines. The key visual contrast is that English has fewer, wider bricks and Portuguese has more, narrower bricks — all at the same height.

---

## 2. The Context Window (the table)

A top-down perspective view of a rectangular table surface with a subtle 3D tilt. The table has a clear fixed border. Inside, three horizontal zones with different colors: left zone (25% width, light blue) labeled "Your input: instructions, history, files"; middle zone (50% width, light yellow, noticeably dimmer) labeled "Reference context"; right zone (25% width, light green) labeled "Response being built". Along the right edge of the table, a small stack of LEGO bricks falls off the edge with a label "Doesn't fit on the table = doesn't exist for the model". Along the bottom edge, a thin gradient bar runs the full width: bright on the left, dim in the middle, bright on the right, with a label beneath: "Model attention: strong at edges, weak in the middle". The table edge is labeled "1M tokens (varies by model)". Flat infographic style, top-down view, clean and minimal.

---

## 3. Autoregressive Generation: one piece at a time

Three-panel illustration showing a LEGO model being built one brick at a time. Flat infographic style, white background.

Panel 1 "Step 1": LEGO bricks labeled "The", "sky", "is" are already placed in a row. An empty spot with "?" next to them. Below, three loose bricks are the options: "blue (25%)", "cloudy (15%)", "clear (12%)". An arrow shows "blue" being chosen.

Panel 2 "Step 2": Now "The", "sky", "is", "blue" are placed. Empty spot with "?". Options below: "and (20%)", "today (15%)", ". (10%)". Arrow shows "today" being chosen.

Panel 3 "Step 3": Now "The", "sky", "is", "blue", "today" are placed. Empty spot with "?". Options below: ". (35%)", ", (12%)". Arrow shows "." being chosen.

Caption at the bottom: "No plan. One piece at a time. Always."

---

## 4. Attention Mechanism: the model lights up what matters

A top-down view of the same rectangular table from illustration 2, now populated with seven LEGO bricks in a row: "The", "bank", "is", "on", "the", "river", "shore". The brick "bank" is highlighted with a bold golden border and slightly elevated. From "bank", radial glow lines emanate outward to each other brick. The lines to "river" and "shore" are thick, bright, and vivid orange. The lines to "The", "is", "on", "the" are thin and very faded gray. The bricks "river" and "shore" glow brightly (orange halo), while the other bricks are dimmer. Above the table: "Which 'bank' is this?". Below the table: "The model lights up the most relevant pieces." A small legend in the corner shows a thick bright line labeled "strong attention" and a thin faded line labeled "weak attention". No directional arrows, only radial glow lines. Flat infographic, warm color palette.

---

## 5. Temperature: how deep the hand reaches into the box

Illustration with a single large LEGO box centered in the image, viewed from the front with a cross-section cut to reveal the interior. All text in English.

The box: rectangular, tall, seen from the front with the front wall removed (cross-section). At the top of the box, the text "Vocabulary" (this text appears ONLY ONCE, only here). Inside the box, pieces are organized in layers from top to bottom: top layer with three large blue LEGO bricks; middle layer with smaller green bricks; lower layer with small mixed-color pieces; and at the very bottom, a single red wheel piece.

Four horizontal dashed lines cut across the box at four depths, each with a label to the right indicating the temperature and behavior:

- Line 1 (at the top of the box, touching the blue bricks): "0.0 — Always the same piece"
- Line 2 (between the blue and green bricks): "0.3 — Small variations"
- Line 3 (in the middle of the box, between the green bricks): "0.7 — Creative"
- Line 4 (at the bottom, touching the red wheel): "1.5 — Incoherent"

A simple robotic arm enters from the top opening of the box. The arm can be positioned at any of the depths.

All labels must be right-aligned to the right of the box, vertically centered on their respective line. Flat infographic style, white background, clean lines. No 2x2 grid, no separate panels. A single composition with a single box.

---

## 6. Model Families: from Duplo to Technic

A horizontal spectrum bar running left to right on a white background. Left end labeled "Faster / cheaper", right end labeled "More capable / more expensive". Above the spectrum, four LEGO kit boxes are positioned at different points along it, each drawn to look like a simplified LEGO product box. Box 1 (far left, light blue): "Fast Models" — shows large simple Duplo-style bricks on the box art. Below: "Haiku · GPT-4o-mini · Flash". Box 2 (center-left, teal): "Code Models" — shows medium regular LEGO bricks. Below: "GPT-4.1 · Sonnet". Box 3 (center-right, dark blue): "Reasoning Models" — shows Technic gears and axles on box art. Below: "Opus · o3-pro · Gemini 2.5 Pro". Box 4 (far right, slightly below the spectrum, green): "Open-weight" — shows an open box with all pieces visible and exposed. Below: "Llama 4 · DeepSeek R1" and "You build, tweak, and adapt." Below the entire spectrum, a rule in bold: "Start with the cheapest that works. Scale up only if needed." Flat infographic style, clean product-box silhouettes.

---

## 7. Limitations: hallucination and clean table

A two-panel illustration. Left panel titled "Hallucinations": A small LEGO building on a table, viewed at a 3/4 angle. The front face of the building looks perfect — neat, colorful, well-assembled bricks forming a complete facade with a door and windows. But the back and side are visible in the 3/4 view, revealing that the building is completely hollow — no back wall, no internal structure, just a facade. An arrow pointing to the front: "Looks correct." An arrow pointing to the hollow back: "No internal verification." Right panel titled "Clean table between conversations": Two stacked scenes separated by a dashed line. Top scene: a table with a complete LEGO construction on it, labeled "Conversation 1 — complete build." Bottom scene: the same table, completely empty and clean, labeled "Conversation 2 — table wiped clean." Between them, a broom icon. Below: "If you need it to remember, you put it back on the table." Flat infographic, clean and impactful.

---

## 8a. Cost: consulting vs building

A side-by-side illustration showing why output tokens cost more than input tokens using the LEGO table metaphor. Left side labeled "Input — consulting": a hand dumps a pile of loose LEGO bricks onto the table surface in one motion — bricks scattered casually, landing in a heap. A small green price tag hangs from the pile: "$3 per 1M pieces". The gesture is fast, effortless, bulk. Right side labeled "Output — building": the same table, but now a robotic arm carefully holds a single brick, placing it precisely onto a growing construction. A spotlight illuminates the entire table surface (representing the full attention pass over all previous tokens). A large red price tag hangs from the arm: "$15 per 1M pieces". Below the arm, a small annotation: "Each piece requires scanning the entire table before placing." Below both sides, a single centered caption: "Consulting is dumping bricks on the table. Building is placing one at a time. That's why output costs 3–5x more." Flat infographic style, same table shape established in previous illustrations, clean and minimal.

---

## 8b. The linguistic tax: three layers, one problem

A vertical cascade of three layers, read top to bottom, each showing the same comparison between English (blue) and Portuguese (orange), with each layer building on the previous one. Layer 1 labeled "More pieces" (callback to section 1): two short horizontal rows of LEGO bricks side by side. The English row has 5 large bricks. The Portuguese row has 8 smaller bricks. Same total row width, different brick count. A small "=" sign between the two final constructions shows they represent the same content. Layer 2 labeled "Less space on the table" (callback to section 2): two identical table surfaces side by side. The English table has ample empty space remaining after placing its bricks. The Portuguese table is noticeably more crowded with the same content taking up more surface area — less breathing room. Layer 3 labeled "Higher bill" (this section): two identical cash register displays or simple receipt slips side by side. The English receipt shows "$100". The Portuguese receipt shows "$135". The Portuguese receipt has a highlighted "+35%" badge. A vertical arrow runs along the left side connecting all three layers, labeled: "Same problem, three layers." At the bottom, a single caption: "Portuguese uses more pieces, fills more table, and costs more. It's not three problems." Flat infographic, clean vertical flow, blue and orange color coding consistent throughout all three layers.
