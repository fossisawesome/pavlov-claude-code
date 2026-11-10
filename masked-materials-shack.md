# How to Improve Masked Materials on Shack

> Source: https://mod.io/g/pavlov/r/masked-materials-shack
> Author: Marco_G17 | Added: 2026-08-30 | Updated: 2026-08-30 | Views: 211 | Comments: 0 | Tags: graphics, materials, performance, Shack
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 5 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Quick guide on how to make masked materials on Shack look better.

---
For best practices for materials in general take a look at [this guide](https://mod.io/g/pavlov/r/best-practices-for-shack-materials).

This guide shows off some simple improvements for masked materials. A few of them are effective even on PC. 

While masked itself is pretty expensive compared to opaque materials on Meta Quest, these techniques don't/barely affect performance. So if you want something to use masked, be sure to check out these methods. 

### Alpha to Coverage

A2C is the most important setting by far, I don't know why this isn't default tbh. This only works on mobile.

This setting basically lets MSAA run on the masked edges, so jagged edges are removed. Worth it when you use masked materials sparingly but performance impact can be argued. No notable performance issues usually. 

![image](images/masked-materials-shack/b4b8959c63.png) <!-- src: https://image.modcdn.io/members/909b/32887797/profile/a2c_guide.png -->

You can clearly see in the image above, using A2C looks far better. 

To enable this setting, open your masked material, navigate to the mobile section > advanced > tick "Use Alpha to Coverage"

![image](images/masked-materials-shack/ad31f99aef.png) <!-- src: https://image.modcdn.io/members/909b/32887797/profile/a2cenable.png -->

### Scale Mips for Alpha Coverage

Not to be confused with alpha to coverage, this method simply scales the alpha in mipmaps so they have better visibility. This makes thin details in masked materials visible from a further distance.

In simple terms this makes the alpha channel brighter.

![image](images/masked-materials-shack/3df8960e63.png) <!-- src: https://image.modcdn.io/members/909b/32887797/profile/alphamipvisibility.png -->

I recommend using a threshold of 0.75 on the alpha channel. Open your texture and scroll down in the details tab to find this setting. Enable "Do Scale Mips for Alpha Coverage" and tweak the alpha value. 

### Adjust Max Alpha

You can also adjust the maximum alpha on your masked texture, this has no impact on performance. This will not work on textures that use binary alpha channels where alpha is either fully black or fully white. (which is more optimized but looks a bit worse). This is because there is no greyscale data between 0 and 1 to scale. 

![image](images/masked-materials-shack/97c7cab43b.png) <!-- src: https://image.modcdn.io/members/909b/32887797/profile/maxalphavisibility.png -->

I recommend tweaking between 1.0 - 10.0 values. Find this setting in texture details. 

 

I hope this guide helped. Here's a screenshot of what my final foliage looks like using all these settings:

![image](images/masked-materials-shack/7d35c10435.png) <!-- src: https://image.modcdn.io/members/909b/32887797/profile/yesa2c.png -->
