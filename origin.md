# Origin for signed content
Web APIs are mostly origin-based, however on FirefoxOS we use an *Extended Origin* which consists of
{appId + isBrowserElement + origin}.

For the signed content has to be of different origin, I've listed the componenets needs to be changed.

* localStorage
  * Filed [Bug 1165214 - DOMStorageManager should use origin as ScopeKey and QuotaKey](https://bugzilla.mozilla.org/show_bug.cgi?id=1165214)
  * ScopeKey is using 'appId:isBrowser:subdomainsDBKey', QuotaDBKey is using 'appId:isBrowser:subdomain:scheme:port'
    see [DOMStorageManager.cpp](https://dxr.mozilla.org/mozilla-central/source/dom/storage/DOMStorageManager.cpp)
  * [Bug 773373 - Implement "localStorage" jars for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=773373),
  * [Bug 786301 - Delete localstorage related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786301)
* indexedDB
  * Filed [Bug 1165217 - Use origin attribute in nsIUsageCallback)(https://bugzilla.mozilla.org/show_bug.cgi?id=1165217)
  * [nsIUsageCallback.idl](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIUsageCallback.idl)
  * [Bug 756645  - Implement "indexedDB jars" for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=756645)
  * [Bug 786295 - Delete IndexedDB related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786295)
* cache storage
  * Filed [Bug 1165219 - Use origin in ManagerId](https://bugzilla.mozilla.org/show_bug.cgi?id=1165219)
  * [blog](https://blog.wanderview.com/blog/2014/12/08/implementing-the-serviceworker-cache-api-in-gecko/) See *Per Origin Manager*
  * ManagerId uses origin+appId+isBrowser
  * [ManagerId.h](https://dxr.mozilla.org/mozilla-central/source/dom/cache/ManagerId.h)
  * [Bug 940273 - Implement Cache and CacheStorage for ServiceWorkers](https://bugzilla.mozilla.org/show_bug.cgi?id=940273)
* [nsIQuotaManager](https://dxr.mozilla.org/mozilla-central/source/dom/quota/nsIQuotaManager.idl)
  * Filed [Bug 1165224 - Use origin in QuotaManager ](https://bugzilla.mozilla.org/show_bug.cgi?id=1163254)
  * Quota per origin [https://dxr.mozilla.org/mozilla-central/source/dom/quota/QuotaManager.cpp#1396]
  * Quota Limit on eTLD+1
* app_cache
  * Filed [Bug 1165256 - use origin for app_cache](https://bugzilla.mozilla.org/show_bug.cgi?id=1165256)
  * [nsIApplicationCacheService.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIApplicationCacheService.idl)
  * [nsIOfflineCacheUpdate.idl](https://dxr.mozilla.org/mozilla-central/source/uriloader/prefetch/nsIOfflineCacheUpdate.idl)
  * [Bug 751754 - Allow separation between the update-available and start-download states in appcache](https://bugzilla.mozilla.org/show_bug.cgi?id=751754)
  * [Bug 786299 - Delete app-cache related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* permission
  * Filed [Bug 1165263 - Use origin for nsIPermissionManager](https://bugzilla.mozilla.org/show_bug.cgi?id=1165263)
  * [nsIPermissionManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermissionManager.idl)
  * [nsIPermission.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsIPermission.idl)
  * [Bug 786296 - Delete permissions related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786296)
  * [Bug 786299 - Delete app-cache related to an app when uninstalled](https://bugzilla.mozilla.org/show_bug.cgi?id=786299)
* cookie
  * Filed [Bug 1165267 - use origin for cookie](https://bugzilla.mozilla.org/show_bug.cgi?id=1165267)
  * Cookies is using {baseDomain, appId, isBrowserElement} as indexed key in cookie.sqlite.
  * [nsICookieManager2.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieManager2.idl)
  * [nsICookieService.idl]((https://dxr.mozilla.org/mozilla-central/source/netwerk/cookie/nsICookieService.idl)
  * [Bug 756648 - Implement "cookie jars" for apps](https://bugzilla.mozilla.org/show_bug.cgi?id=756648)
  * [Bug 783408 - Delete cookiejar when we remove a B2G app](https://bugzilla.mozilla.org/show_bug.cgi?id=783408)
* http cache
  * Filed [Bug 1165269 - Use origin for http cache](https://bugzilla.mozilla.org/show_bug.cgi?id=1165269)
  * [nsILoadContextInfo.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/base/nsILoadContextInfo.idl)
  * [nsIHttpAuthManager.idl](https://dxr.mozilla.org/mozilla-central/source/netwerk/protocol/http/nsIHttpAuthManager.idl)
  * [Bug 913807 - Land HTTP cache v2 pref'ed off](https://bugzilla.mozilla.org/show_bug.cgi?id=913807)
* csp
  * [nsIContentPolicy.idl](https://dxr.mozilla.org/mozilla-central/source/dom/base/nsIContentPolicy.idl) still uses nsIURI instead of nsIPrincipal.
  * uses prepath for certified apps.[DXR](https://dxr.mozilla.org/mozilla-central/source/dom/security/nsCSPService.cpp#147)
  * prepath will be removed in [Bug 1030936 - \[CSP\] remove fast-path for certified apps once the C++ backend is activated](https://bugzilla.mozilla.org/show_bug.cgi?id=1030936)
* service worker
  * See [Bug 1162088 - ServiceWorker is reused between apps with the same origin](https://bugzilla.mozilla.org/show_bug.cgi?id=1162088)
* broadcast_channel
  * Filed [Bug 1165270 - Use origin for BroadcastChannel](https://bugzilla.mozilla.org/show_bug.cgi?id=1165270)
  * BroadcastChannel uses manifestURL for the origin
  * [BroadcastChannel#GetOrigin](https://dxr.mozilla.org/mozilla-central/source/dom/broadcastchannel/BroadcastChannel.cpp#53)
  * [Bug 966439 - Implement BroadcastChannel API](https://bugzilla.mozilla.org/show_bug.cgi?id=966439)
* [nsIScriptSecurityManager.idl](https://dxr.mozilla.org/mozilla-central/source//caps/nsIScriptSecurityManager.idl)
  * Filed [Bug 1165272 - use origin for nsIScriptSecurityManager](https://bugzilla.mozilla.org/show_bug.cgi?id=1165272)
  * [Bug 774585 - Update GetCodebasePrincipal callers to use the correct "data jar"](https://bugzilla.mozilla.org/show_bug.cgi?id=774585)
* [nsIPrincipal.idl](https://dxr.mozilla.org/mozilla-central/source/caps/nsIPrincipal.idl)
  * Filed [Bug 1165277 - Use origin in SessionStorage.jsm](https://bugzilla.mozilla.org/show_bug.cgi?id=1165277)
  * jarPrefix(appId + isBrowserElement) is used by [shared-pool](https://bugzilla.mozilla.org/show_bug.cgi?id=785884)
* [nsIDocShell.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsIDocShell.idl)
* [nsILoadContext.idl](https://dxr.mozilla.org/mozilla-central/source/docshell/base/nsILoadContext.idl)

# Consumers for nsIPrincipal needs to be updated.
* calling nsIPrincipal.subsumes/equals
  * TBD (Will bholley change the signature of nsIPrincipal.subsume()?)
* calling nsIPrincipal.origin
  * TBD (will origin contain 'signedAppName' ?)
* places may have problems on checking origins without using interfaces of nsIPrincipal.
  * TBD (can Jonas/Bholley provide some examples about wrong usage?)
  * docshell/base/nsDocShell.cpp # AddSessionStorage

