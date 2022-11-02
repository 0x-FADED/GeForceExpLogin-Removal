# GeForceExpLogin-Removal
Remove Mandatory Login of Geforce Experience - [support: v3.26.0.154 and higher]
# How to Remove Mandatory Login  

make a backup of every files you edit !

# Easy copy/paste fix :  

Download pre-moded app.js : [https://github.com/0x-FADED/GeForceExpLogin-Removal/blob/master/app.js](https://github.com/0x-FADED/GeForceExpLogin-Removal/raw/master/app.js)

Copy/paste to :

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

# Manual way :  
NOTE: some of the code below might change (function letters), just compare with one of the previously uploaded app.js ;)  

use [http://jsbeautifier.org/](http://jsbeautifier.org/) on app.js found in :  

    C:\Program Files\NVIDIA Corporation\NVIDIA GeForce Experience\www\

&#x200B;

1. Nullify login (in app.js)  

\- find :  

    if (e.domains.list.indexOf(n) > -1) return !0

\- replace by :  

    if (e.domains.list.indexOf(n) > -1) return b.handleLoggedIn(e), !0

Now let's add some fake infos, find :
  
            }, b.isLeftPaneVisible = function() {
                return !("choose" === b.nvActiveAuthView)
            }

And replace with this : 

            }, b.isLeftPaneVisible = function() {
                return !("choose" === b.nvActiveAuthView)
            }, b.handleLoggedIn({
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

    Y.isShareSupported = !1, Y.isShareButtonClicked = !1

by

    Y.isShareSupported = !0, Y.isShareButtonClicked = !0

To make the shadowplay & share buttons show on the main GFE screen

&#x200B;

\- Optional (might help in some case where user previously was logged in) find   


    b.info("automatically resent verification email"), u.endActionAsync(r, "EMAIL_NOT_VERIFIED"), h.showEmailVerification(e)  

\-  and remove  

    , h.showEmailVerification(e)

# How to Block Data Collection / Telemetry (block all or keep Games Optimisations)

Step 1 - Open the hosts file in a text editor (notepad++) :

    C:\Windows\System32\drivers\etc\hosts 

(copy-paste the file on your desktop to edit, copy back to "etc" folder if you have permission errors)

Step 2 - Add at the end of the file (CHOOSE ONE OR THE OTHER LIST, NOT BOTH) :  
> Full blocklist: blocks telemetry / driver & Gfe updates (Keeps Game Optimisations and all "offline" features working)
> Lite blocklist : only blocks telemetry (might break Game Optimisations in some cases, fix/workaround pending)

- FULL BLOCKLIST : (as of 04/17/2020 - GFE 3.20.3.63)  

`0.0.0.0 telemetry.gfe.nvidia.com`  
`0.0.0.0 gfe.nvidia.com`  
`0.0.0.0 gfwsl.geforce.com`  
`0.0.0.0 services.gfe.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.cn`  
`0.0.0.0 events.gfe.nvidia.com`  
`0.0.0.0 img.nvidiagrid.net`  
`0.0.0.0 images.nvidiagrid.net`  
`0.0.0.0 images.nvidia.com`  
`0.0.0.0 ls.dtrace.nvidia.com`  
`0.0.0.0 ota.nvidia.com`  
`0.0.0.0 ota-downloads.nvidia.com`  
`0.0.0.0 rds-assets.nvidia.com`  
`0.0.0.0 assets.nvidiagrid.net`  
`0.0.0.0 nvidia.tt.omtrdc.net`  
`0.0.0.0 api.commune.ly`  
`0.0.0.0 login.nvgs.nvidia.com`  
`0.0.0.0 login.nvgs.nvidia.cn`  


- LITE BLOCKLIST (keep GFE / Drivers Update working) : (as of 04/17/2020 - GFE 3.20.3.63)  

    might break Game List for now, use the full blocklist if it does

`0.0.0.0 ls.dtrace.nvidia.com`  
`0.0.0.0 telemetry.gfe.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.com`  
`0.0.0.0 accounts.nvgs.nvidia.cn`  
`0.0.0.0 nvidia.tt.omtrdc.net`  
`0.0.0.0 api.commune.ly`  
`0.0.0.0 login.nvgs.nvidia.com`  
`0.0.0.0 login.nvgs.nvidia.cn`  

("[0.0.0.0](https://0.0.0.0)" is preferred to "[127.0.0.1](https://127.0.0.1)" but both works)  
( If you previously blocked all nvidia domains, you need to flush your dns cache to restore "Game Optimizations" functionality :  
open "CMD" > `ipconfig /flushdns` )

Save and forget :)  

&#x200B;

PS: The "beautified" version of app.js will work just fine, you can minify it back, but it's not mandatory (just like login :) ).

*Post and fix based off the previous mod author(s), mainly :* [*https://www.reddit.com/r/nvidia/comments/8b5nej/updated\_remove\_mandatory\_login\_of\_geforce/*](https://www.reddit.com/r/nvidia/comments/8b5nej/updated_remove_mandatory_login_of_geforce/)
