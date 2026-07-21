# Cache

Thin wrapper around [aplus-framework/cache](https://docs.aplus-framework.com/guides/libraries/cache/index.html) that puts each backend behind `orange\framework\interfaces\CacheInterface`, so application code can depend on the interface instead of a specific backend.

## Example

```php
use orange\cache\FilesCache;

// $config is passed straight through to the aplus-framework backend
// (for FilesCache, an array with a 'directory' key)
$cache = FilesCache::getInstance($config);

$cache->set('homepage.stats', ['visits' => 42], 300); // ttl in seconds
$stats = $cache->get('homepage.stats');                // null if missing/expired

$cache->delete('homepage.stats');
$cache->flush(); // clear everything
```

Swap `FilesCache` for `RedisCache`, `MemcachedCache`, `IncludeCache`, or `DummyCache` (a no-op cache, useful for tests or disabling caching entirely) — each implements the same `get`/`set`/`delete`/`flush` contract and is retrieved via its own `getInstance($config)`.
