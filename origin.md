# Origin for signed package content
* localStorage
  * Key is using 'appId:t/f:subdomainsDBKey'
    see [DOMStorageManager.cpp](https://dxr.mozilla.org/mozilla-central/source/dom/storage/DOMStorageManager.cpp#199)
  * [Bug 773373](https://bugzilla.mozilla.org/show_bug.cgi?id=773373), [Bug 786301](https://bugzilla.mozilla.org/show_bug.cgi?id=786301)
* indexedDB
  * [nsIQuotaManager](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIQuotaManager.idl)
  * [nsIUsageCallback.idl](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIUsageCallback.idl)
  * [Bug 756645](https://bugzilla.mozilla.org/show_bug.cgi?id=756645) [Bug 786295](https://bugzilla.mozilla.org/show_bug.cgi?id=786295)
* app_cache
  * [nsIApplicationCacheService.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIApplicationCacheService.idl)
  * [nsIOfflineCacheUpdate.idl](https://dxr.mozilla.org/mozilla-central/source/uriloader/prefetch/nsIOfflineCacheUpdate.idl)
  * [Bug 751754](https://bugzilla.mozilla.org/show_bug.cgi?id=751754) [Bug 786299](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* permission
  * [nsIPermissionManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermissionManager.idl)
  * [nsIPermission.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermission.idl)
  * [Bug 786296](https://bugzilla.mozilla.org/show_bug.cgi?id=786296) [Bug 786299](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* cookie
  * Cookies is using {baseDomain, appId, isBrowserElement} as indexed key in cookie.sqlite.
  * [nsICookieManager2.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieManager2.idl)
  * [nsICookieService.idl]((https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieService.idl)
  * [Bug 756648](https://bugzilla.mozilla.org/show_bug.cgi?id=756648) [Bug 783408](https://bugzilla.mozilla.org/show_bug.cgi?id=783408)
* http cache
  * [nsILoadContextInfo.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsILoadContextInfo.idl)
  * [nsIHttpAuthManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/protocol/http/nsIHttpAuthManager.idl)
  * [Bug 913807](https://bugzilla.mozilla.org/show_bug.cgi?id=913807) [Bug 783408](https://bugzilla.mozilla.org/show_bug.cgi?id=783408)
* [nsIScriptSecurityManager.idl](https://dxr.mozilla.org/mozilla-central/source//caps/nsIScriptSecurityManager.idl)
  * [Bug 774585](https://bugzilla.mozilla.org/show_bug.cgi?id=774585)
* [nsIPrincipal.idl](https://dxr.mozilla.org/mozilla-central/source/caps/nsIPrincipal.idl)
* [nsIDocShell.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsIDocShell.idl)
* [nsILoadContext.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsILoadContext.idl)
