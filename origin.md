# Origin for signed content
Web APIs are mostly origin-based, however on FirefoxOS we use an *Extended Origin* which consists of
{appId + isBrowserElement + origin}.

For the signed content has to be of different origin, I've listed the componenets needs to be changed.

* localStorage
  * ScopeKey is using 'appId:isBrowser:subdomainsDBKey', QuotaDBKey is using 'appId:isBrowser:subdomain:scheme:port'
    see [DOMStorageManager.cpp](https://dxr.mozilla.org/mozilla-central/source/dom/storage/DOMStorageManager.cpp)
  * [Bug 773373 - Implement "localStorage" jars for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=773373),
  * [Bug 786301 - Delete localstorage related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786301)
* indexedDB
  * [nsIUsageCallback.idl](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIUsageCallback.idl)
  * [Bug 756645  - Implement "indexedDB jars" for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=756645)
  * [Bug 786295 - Delete IndexedDB related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786295)
* cache storage
  * [blog](https://blog.wanderview.com/blog/2014/12/08/implementing-the-serviceworker-cache-api-in-gecko/) See *Per Origin Manager*
  * ManagerId uses origin+appId+isBrowser
  * [ManagerId.h](https://dxr.mozilla.org/mozilla-central/source/dom/cache/ManagerId.h)
  * [Bug 940273 - Implement Cache and CacheStorage for ServiceWorkers](https://bugzilla.mozilla.org/show_bug.cgi?id=940273)
* [nsIQuotaManager](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIQuotaManager.idl)
  * Quota per origin [https://dxr.mozilla.org/mozilla-central/source/dom/quota/QuotaManager.cpp#1396]
  * Quota Limit on eTLD+1
* app_cache
  * [nsIApplicationCacheService.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIApplicationCacheService.idl)
  * [nsIOfflineCacheUpdate.idl](https://dxr.mozilla.org/mozilla-central/source/uriloader/prefetch/nsIOfflineCacheUpdate.idl)
  * [Bug 751754 - Allow separation between the update-available and start-download states in appcache](https://bugzilla.mozilla.org/show_bug.cgi?id=751754)
  * [Bug 786299 - Delete app-cache related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* permission
  * [nsIPermissionManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermissionManager.idl)
  * [nsIPermission.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermission.idl)
  * [Bug 786296 - Delete permissions related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786296)
  * [Bug 786299 - Delete app-cache related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* cookie
  * Cookies is using {baseDomain, appId, isBrowserElement} as indexed key in cookie.sqlite.
  * [nsICookieManager2.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieManager2.idl)
  * [nsICookieService.idl]((https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieService.idl)
  * [Bug 756648 - Implement "cookie jars" for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=756648)
  * [Bug 783408 - Delete cookiejar when we remove a B2G app](https://bugzilla.mozilla.org/show_bug.cgi?id=783408)
* http cache
  * [nsILoadContextInfo.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsILoadContextInfo.idl)
  * [nsIHttpAuthManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/protocol/http/nsIHttpAuthManager.idl)
  * [Bug 913807 - Land HTTP cache v2 pref'ed off](https://bugzilla.mozilla.org/show_bug.cgi?id=913807)
* csp
  * [nsIContentPolicy.idl](https://dxr.mozilla.org/mozilla-central/source/dom/base/nsIContentPolicy.idl) still uses nsIURI instead of nsIPrincipal.
  * uses prepath for certified apps.[DXR](https://dxr.mozilla.org/mozilla-central/source/dom/security/nsCSPService.cpp#147)
* broadcast_channel
  * BroadcastChannel uses manifestURL for the origin
  * [BroadcastChannel#GetOrigin](https://dxr.mozilla.org/mozilla-central/source/dom/broadcastchannel/BroadcastChannel.cpp#53)
  * [Bug 966439 - Implement BroadcastChannel API](https://bugzilla.mozilla.org/show_bug.cgi?id=966439)
* [nsIScriptSecurityManager.idl](https://dxr.mozilla.org/mozilla-central/source//caps/nsIScriptSecurityManager.idl)
  * [Bug 774585 - Update GetCodebasePrincipal callers to use the correct "data jar"](https://bugzilla.mozilla.org/show_bug.cgi?id=774585)
* [nsIPrincipal.idl](https://dxr.mozilla.org/mozilla-central/source/caps/nsIPrincipal.idl)
  * jarPrefix(appId + isBrowserElement) is used by [shared-pool](https://bugzilla.mozilla.org/show_bug.cgi?id=785884)
* [nsIDocShell.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsIDocShell.idl)
* [nsILoadContext.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsILoadContext.idl)
