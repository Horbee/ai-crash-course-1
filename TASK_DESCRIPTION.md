# About the Banknotes Dataset

> "If you look at a dollar bill under a microscope, it looks like a mountain range of ink. If you look at a fake, it looks like a flat swamp of dots. This AI doesn't 'see' the face of the president; it 'feels' the roughness of the mountains."

This dataset wasn't created by manually measuring banknotes with a ruler. It comes from a study at the **University of Applied Sciences Ostwestfalen-Lippe (Germany)**.

Because professional printing is so physically different from home printing, a neural network (even a small one) can separate these classes very easily. You should expect very high accuracy (98-100%).

- **The Source:** They took about 1,372 banknotes. Some were genuine, and others were high-quality forgeries.
- **The Process:** They didn't just take iPhone photos. They used an industrial-grade camera (usually used for print inspection) to digitize the banknotes into **grayscale images** at a high resolution (660 dpi).
- **The Problem:** A 400x400 pixel image has 160,000 data points (pixels). That is too large and noisy for a simple model. They needed to summarize the "texture" of the paper into just a few numbers.
- **The Solution (Wavelet Transform):** They used a mathematical tool called the **Wavelet Transform**. Think of this like a microscope that breaks an image down into its horizontal, vertical, and diagonal edges. It separates the "coarse" info (the general shape of the bill) from the "fine" info (the sharp, tiny security details).

### 2. Decoding the Features (The "Translation")

what the inputs are: _Is the image sharp? Is it complex? Is the contrast high?_

Authentic banknotes use **Intaglio printing** (raised ink) and micro-printing, creating extremely sharp, crisp lines. Counterfeits, often made with laser or inkjet printers, are "fuzzier" or have "dithering" noise (tiny dots) where there should be solid lines.

The four features measure this difference in texture:

| Feature      | The Math Definition                            | The "Banknote" Meaning                                                                                                                                                                                                        |
| ------------ | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Variance** | How spread out the values are.                 | **"Contrast Intensity."** High variance usually means the image has strong, bold edges and high contrast (like crisp security ink). Low variance implies a washed-out or blurry image.                                        |
| **Skewness** | How asymmetrical the data is.                  | **"Light vs. Dark Balance."** Authentic notes often have a specific balance of light paper and dark ink. A photocopy might turn dark gray areas into black blobs, skewing the histogram of the image data.                    |
| **Kurtosis** | How "heavy" the tails of the distribution are. | **"Sharpness of Edges."** This detects sudden changes. A real banknote has very sudden transitions (Paper Ink). A fake one has softer transitions (Paper blurry edge Ink). Kurtosis captures these "outliers" or sharp jumps. |
| **Entropy**  | The randomness or disorder in the pixels.      | **"Complexity."** Real banknotes are incredibly complex (random-looking security patterns). A fake might lose this detail and look "smoother" or more uniform, having lower entropy.                                          |
