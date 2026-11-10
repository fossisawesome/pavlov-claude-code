# Dynamic Zoom for Scopes

> Source: https://mod.io/g/pavlov/r/dynamic-zoom-component-guide
> Author: DarkAtツ | Added: 2024-05-28 | Updated: 2024-05-28 | Views: 352 | Comments: 0 | Tags: AdjustableZoom, Attachment, DynamicZoom, Scope
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 3 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A guide on how to add a dynamic zoom functionality to scopes.

---
Guide Preview Image from [CodeLikeMe](https://youtu.be/RX_3lQsPX_k)

#### Pre-Setup

1.1. Add this source plugin to your modkit: [[Source] DarkAt26 (UGC3945378)](https://mod.io/g/pavlov/m/darkat26)

1.2. Copy or move the DynamicZoomComponent component to your own ugc to be independant of the source plugin mod. You can also add the source plugin mod as a dependency and not move the component; i only recommend this for testing as the structure in the source plugin mod might change.

### Setup

#### DynamicZoomComponent

2.1. Open your scope bp and add the component DynamicZoomComponent to it.

2.2. Trigger the OnGunTickChanged function from the DynamicZoomComponent when the Event On Gun Tick Changed gets triggered in the scope. Also connect the Enabled pin of the event to the function.

![image](images/dynamic-zoom-component-guide/8db04080e7.jpg) <!-- src: https://image.modcdn.io/members/7c1e/5313379/profile/screenshot2024-05-28190958.jpg -->

2.3. Click on the DynamicZoomComponent in the Components list and change the FOV value in the Details tab which is responsible for the zoom to a value that you want.

![image](images/dynamic-zoom-component-guide/ebe79d58ec.jpg) <!-- src: https://image.modcdn.io/members/7c1e/5313379/profile/screenshot2024-05-28191507.jpg -->

2.4. The FOV value can be adjusted via BP code on runtime if needed.

#### Activation

3. You can use the component activation to enable and disable the component.

3.1 bAutoActivate is disabled by default as it would be best to have the default zoom/fov set in the scope directly, additional zoom values should be handled by the component. You can also enable bAutoActivate if needed by just checking the box for it in the component.

3.2. The Set Active, Activate, Deactivate and Toggle Activate nodes can be used on the DynamicZoomComponent to enable/disable the zoom changes. To have the scope in the default zoom the component should be deactivated.

![image](images/dynamic-zoom-component-guide/f7b5f7bb90.jpg) <!-- src: https://image.modcdn.io/members/7c1e/5313379/profile/screenshot2024-05-28192402.jpg -->
