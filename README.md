# Optical-Character-Recognition

Extracting embedded text in images using MATLAB

Procedure:
Step 1: Detect Candidate Text Regions Using MSER The MSER feature
detector works well for finding text regions . It works well for text because the
consistent color and high contrast of text leads to stable intensity profiles.The
detectMSERFeatures function is used to find all the regions within the image
and plot these results.There may be many non text region alongside of the
image.
Step 2: Remove Non-Text Regions Based On Basic Geometric Properties
Although the MSER algorithm picks out most of the text, it also detects
many other stable regions in the image that are not text. We can use a
rule-based approach to remove non-text regions. For example, geometric
properties of text can be used to filter out non-text regions using simple
thresholds. Alternatively, we can use a machine learning approach to train a
text vs. non-text classifier. Typically, a combination of the two approaches
produces better results . This example uses a simple rule-based approach
to filter non-text regions based on geometric properties. Use regionprops to
measure a few of these properties and then remove regions based on their
property values.
Step 3: Remove Non-Text Regions Based On Stroke Width Variation
Another common metric used to discriminate between text and non-text is
stroke width. Stroke width is a measure of the width of the curves and
lines that make up a character. Text regions tend to have little stroke width
variation, whereas non-text regions tend to have larger variations.
Step 4: Merge Text Regions For Final Detection Result At this point, all
the detection results are composed of individual text characters. To use these
results for recognition tasks, such as OCR, the individual text characters
must be merged into words or text lines. This enables recognition of the
actual words in an image, which carry more meaningful information than
just the individual characters. For example, recognizing the string 'EXIT' vs.
the set of individual characters 'X','E','T','I', where the meaning of the word
is lost without the correct ordering. One approach for merging individual
text regions into words or text lines is to first find neighboring text regions
and then form a bounding box around these regions. To find neighboring
regions, expand the bounding boxes computed earlier with regionprops. This
makes the bounding boxes of neighboring text regions overlap such that text
regions that are part of the same word or text line form a chain of overlapping
bounding boxes.
Step 5: Recognize Detected Text Using OCR After detecting the text
regions, use the ocr function to recognize the text within each bounding box.
Note that without first finding the text regions, the output of the ocr function
would be considerably more noisy.
