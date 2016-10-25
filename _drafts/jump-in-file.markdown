---
title:  "Xcode · Jumping Within Files"
description: A.K.A. Bookmarking / Last Edit Location
## date: add a date when publishing
---

**Use Case**: The layout of some big file requires you to scroll a lot to look-up stuff while coding. Ideally, you'd have a shortcut to jump to your _last edit location_ (like in most IDEs out there) or jump between bookmarks… 

**Approach**: If there had been an existing Xcode option for this, I would post it here. Unfortunately, we'll have to mimick a bookmark using a temporary code snippet.


***

### Code Snippet Placeholders
From my [previous post on making Xcode snippets][post-on-xcode-snippets] you know that these can be quickly inserted & that you can jump between the placeholder fields using **Ctr /** 
…regardless if these placeholder fields are many lines of code apart!
It's like dropping a breadcrumb.

##### Positives
• This will work in any version of Xcode (6, 7, 8), because we use the native Xcode functionality.

##### Negatives
-- It requires the developer to remove the placeholder before building, else Xcode will complain. 
-- If your workflow involves many small changes and re-builds the removal of the placeholders can become tedious. In practice, I'd expect you wouldn't need too many though.
   
⁇ can allow builds including placeholders? If so, cleaning up before submitting a PR would be the time to remove them, together with any debug stuff. 

-- You might have other snippets and don't want this snippet taking up space in the auto-complete box.

***

The bottom line is that we should have an _actual_ Xcode option to do this, and until we do it's up to you to determine if any of the workarounds here are worth it.


[post-on-xcode-snippets]: http://paul-van-klaveren.github.io/2015/deriving-framework-version/
