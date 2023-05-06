---
title: "How to make ios like a photo gallery using framer motion?"
datePublished: Sat May 06 2023 12:59:50 GMT+0000 (Coordinated Universal Time)
cuid: clhbzsiiy000009mgb117eza9
slug: how-to-make-ios-like-a-photo-gallery-using-framer-motion
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683377613076/e24bac82-882e-4223-8354-306f410a8d0b.webp
tags: javascript, animation, reactjs, framer-motion

---

Hello everyone, I'm [Apoorv](https://twitter.com/apoorv_taneja), currently working as a senior frontend engineer at Razorpay.

Lately, I've been exploring Framer and building quick prototypes. In this blog, I'll explain how to create an iOS-like photo gallery easily using Framer Motion.

### A quick demo 🪄

<iframe src="https://stackblitz.com/edit/ios-gallery?embed=1&file=src/App.tsx&view=preview" width="800" height="700"></iframe>

### Let's begin 👨🏻‍💻

To use images for the gallery, we would be using `https://picsum.photos/id/` URL for generating random images.

As you may have noticed in the demo, when you click on an image, it expands and takes up the entire width and height of the container. When you click on the expanded image, it animates back to its original position. This animation behaviour is similar to that of the iOS photo gallery.

To implement this behaviour, we'll use a prop called, which is provided by the Framer `Motion` component. It is useful when a component is removed from a React tree and added back to the tree, as it animates from the previous component's bounding box and its latest animated values.

If you didn't understand what that means, don't worry I'll explain in the later part of the blog.

Let's iterate over the images and render them.

```javascript
      <motion.div
        className="flex flex-wrap gap-1 image-container relative"
        layout
      >
        {imageIds.map((i) => {
            return (
              <motion.div className="w-24 h-24" key={i}>
                <motion.img
                  layoutId={`img-${i}`}
                  src={`https://picsum.photos/id/${i}/800`}
                  onClick={() => openImage(i)}
                />
              </motion.div>
            );
          })}
      </motion.div>
```

When you click on an image, we want it to expand and take up the entire width and height. To achieve this, we can store the image ID in the state and then render it:

```javascript
{selectedImage ? (
  <motion.img
    layoutId={`img-${selectedImage}`}
    src={`https://picsum.photos/id/${selectedImage}/800`}
    className="animate-open-image"
    onClick={() => setSelectedImage(null)}
  />
) : null}
```

Now combining these two code pieces

```javascript
      <motion.div
        className="flex flex-wrap gap-1 image-container relative"
        layout
      >
        {imageIds.map((i) => {
          return (
            <motion.div className="w-24 h-24" key={i}>
              <motion.img
                layoutId={`img-${i}`}
                src={`https://picsum.photos/id/${i}/800`}
                onClick={() => openImage(i)}
              />
            </motion.div>
          );
        })}
        {selectedImage ? (
          <motion.img
            layoutId={`img-${selectedImage}`}
            src={`https://picsum.photos/id/${selectedImage}/800`}
            className="animate-open-image"
            onClick={() => setSelectedImage(null)}
          />
        ) : null}
      </motion.div>
```

In the iOS gallery, there's a spring-type animation when you click on an image. The image scales slightly and then takes up the entire width and height. To add that to our code, we can use `transition={{ duration: 0.4, type: 'spring' }}`.

We've also added a class `animate-open-image` to apply the following styles when the image component is rendered:

```css
.animate-open-image {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

### How does this work?

We utilized the `layoutId` prop while rendering all the images. When an image is clicked, it is given the same `layoutId` as it had when initially rendered.

```javascript
layoutId={`img-${i}`} and layoutId={`img-${selectedImage}`}
```

When the expanded image is clicked, the `selectedImage` state variable becomes null, causing the expanded image to be removed from the React tree and animated back to its original position. The `layoutId` prop is crucial in animating the image back to its original position when it is removed from the tree. And that's how this animation is working.

---

That's all for this blog. I hope you found this blog helpful and informative. I'll be sharing more blogs around framer motion in the coming days. 🎉

Feel free to play around with the embedded demo above. 🛠

If you have any questions, feel free to reach out to me on [Twitter](https://twitter.com/apoorv_taneja), [GitHub](https://github.com/plxity)