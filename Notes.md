# Dataset

## refs(umd).p

The `refs(umd).p` file splits the dataset into three parts:
* Train (`img['split'] == 'train'`) - 42226 examples
* Val (`img['split'] == 'val'`) - 2573 examples
* Test (`img['split'] == 'test'`) - 5023 examples

For a total of 49822 examples.

Each object in `refs(umd).p` contains the following attribute: `'file_name': 'COCO_train2014_000000380440_491042.jpg'`.
It is _not_ the actual image name. The actual image name is that obtained by removing the last part (_e.g._ `_491042`). The last part (the number following the last underscore) is the same as the attribute `ann_id`.

The attribute `image_id` uniquely identifies each image. There can be, indeed, more than one instance with the same `image_id` because the actual image is the same with different description/prompts/referring expressions.

Grouping images by `image_id` shows that there are 25799 different/distinct images.

Each image can have many `sentences`, that is prompts describing the content of the bounding box (note: the bounding box is instead located in the `instances.json` file). Computing the number of distinct images (that is, 25799, as shown above), computing the number of overall prompts, and dividing the latter by the former number gives ~3.7 (that is, there's an average of 3.7 referring expressions per image).


## instances.json

It is a dictionary, made up of five top-level objects:
* `info`
* `images`
* `licences`
* `annotations`
* `categories`

The `images` objects contains 25799 elements, therefore it is quite likely it contains a reference/description of each image.

Each object in `images` represents an image. It looks like they all share the same structure. They have 8 attributes, among which:
* `file_name`: it seems the actual file name (not as that in `refs(umd).p`!)
* `id`: it corresponds to the `image_id` attribute found in the objects loaded from the pickle

The attribute `categories` contains 80 elements, one per category. Each category has an associated `id` and a `supercategory` (which, in case of "base" categories, seems to correspond to the category `name`).

There are 208960 `annotations`. Each annotations contains:
* `segmentation`
* `area`
* `iscrowd`
* `image_id`: it corresponds to the `image_id` attribute found in the objects loaded from the pickle
* `bbox`: the bounding box. It is an array of four values, likely to be [top_left_x, top_left_y, width, height]
* `category_id`: it corresponds to the `id` attribute of the category
* `id`: a unique id for the annotation (indeed, there are 208960 distinct ids)