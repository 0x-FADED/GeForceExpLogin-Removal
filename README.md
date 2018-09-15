# BaiGfe
Remove Mandatory Login of Geforce Experience - [support: v3.14.1.48]

# How to Remove Mandatory Login  

make a backup of every files you edit !

# Easy copy/paste fix :  

Download pre-moded app.js : [https://github.com/Moyster/BaiGfe/raw/master/app.js](https://github.com/Moyster/BaiGfe/raw/master/app.js)

Copy/paste to :

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

# Manual way : 

use [http://jsbeautifier.org/](http://jsbeautifier.org/) on app.js found in :  

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

1. Nullify login (in app.js)  

\- find :  

    if (e.domains.list.indexOf(n) > -1) return !0

\- replace by :  

    if (e.domains.list.indexOf(n) > -1) return w.handleLoggedIn(e), !0

Now let's add some fake infos, find :  

                    return !("choose" === w.nvActiveAuthView && C)
                }, b()

After "b()" add a new line and copy/paste this : 

                w.handleLoggedIn({
                    sessionToken: "dummySessionToken",
                    userToken: "dummyUserToken",
                    user: {
                        core: {
                            displayName: "Anonymous",
                            primaryEmailVerified: true
                        }
                    }
                });

&#x200B;

2. Force-enable ShadowPlay and Share buttons :

\-  find and replace

    K.isShareSupported = !1, K.isShareButtonClicked = !1

by

    K.isShareSupported = !0, K.isShareButtonClicked = !0

To make the shadowplay & share buttons show on the main GFE screen

&#x200B;

# How to Block Data Collection / Telemetry

Step 1 - Open the hosts file in a text editor (notepad++) :

    C:\Windows\System32\drivers\etc\hosts 

(copy-paste the file on your desktop to edit, copy back to "etc" folder if you have permission errors)

Step 2 - Add at the end of the file :

    0.0.0.0 telemetry.gfe.nvidia.com
    0.0.0.0 gfe.nvidia.com
    0.0.0.0 services.gfe.nvidia.com
    0.0.0.0 accounts.nvgs.nvidia.com
    0.0.0.0 events.gfe.nvidia.com
    0.0.0.0 images.nvidiagrid.net
    0.0.0.0 rds-assets.nvidia.com
    0.0.0.0 assets.nvidiagrid.net  

("[0.0.0.0](https://0.0.0.0)" is preferred to "[127.0.0.1](https://127.0.0.1)" but both works)  

Save and forget :)  

&#x200B;

PS: The "beautified" version of app.js will work just fine, you can minify it back, but it's not mandatory (just like login :) ).

*Post and fix based off the previous mod author(s), mainly :* [*https://www.reddit.com/r/nvidia/comments/8b5nej/updated\_remove\_mandatory\_login\_of\_geforce/*](https://www.reddit.com/r/nvidia/comments/8b5nej/updated_remove_mandatory_login_of_geforce/)
