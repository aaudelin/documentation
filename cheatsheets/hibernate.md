# Hibernate avec Spring

## Utiliser le second level cache

### Sur les entités

Propriétés :

```java
hibernate.cache.use_second_level_cache=true
hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory
```

Dans l'entité :

```java
@Cacheable
@org.hibernate.annotations.Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class Entity {}
```

### Sur les queries

Attention : en cas de save, le cache sera flushé. L'enregistrement des modifications est valable tant que le save n'est pas exécuté

```java
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
@QueryHints(@QueryHint(name = "org.hibernate.cacheable", value = "true"))
Entity findById(Integer id);
```

## Annexes

Vérifier que le cache fonctionne

```java
Foo foo = new Foo();
fooService.create(foo);
fooService.findOne(foo.getId());
int size = CacheManager.ALL_CACHE_MANAGERS.get(0)
  .getCache("org.baeldung.persistence.model.Foo").getSize();
assertThat(size, greaterThan(0));
```

Les stratégies de cache

- READ_ONLY: Used only for entities that never change (exception is thrown if an attempt to update such an entity is made). It is very simple and performant. Very suitable for some static reference data that don’t change
- NONSTRICT_READ_WRITE: Cache is updated after a transaction that changed the affected data has been committed. Thus, strong consistency is not guaranteed and there is a small time window in which stale data may be obtained from cache. This kind of strategy is suitable for use cases that can tolerate eventual consistency
- READ_WRITE: This strategy guarantees strong consistency which it achieves by using ‘soft’ locks: When a cached entity is updated, a soft lock is stored in the cache for that entity as well, which is released after the transaction is committed. All concurrent transactions that access soft-locked entries will fetch the corresponding data directly from database
- TRANSACTIONAL: Cache changes are done in distributed XA transactions. A change in a cached entity is either committed or rolled back in both database and cache in the same XA transaction

## Liens 

- Général : https://www.baeldung.com/hibernate-second-level-cache
- Sur les hints pratiques : https://thoughts-on-java.org/11-jpa-hibernate-query-hints-every-developer-know/

