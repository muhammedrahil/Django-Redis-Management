# DJANGO-REDIS
DJANGO-REDIS



redis use store a chash memory


1 - install pip install django-redis

2 - download github msi redis
https://github.com/MicrosoftArchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.msi

3 - redis check cmd - redis-cli 

defult port : 127.0.0.1:6379 - 

cmd - redis-cli
type : ping 
output : pong

settings************************************

CACHE_TTL = 60 * 1500

# redis cashe

CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}


views************************************


from django.conf import settings
from django.core.cache.backends.base import DEFAULT_TIMEOUT
from django.views.decorators.cache import cache_page
from django.core.cache import cache
CACHE_TTL = getattr(settings ,'CACHE_TTL' , DEFAULT_TIMEOUT)

       if cache.get('pk'):
            try:
                print("DATA COMING FROM CACHE")
                context = cache.get('pk')   
            except:
                print("DATA COMING FROM DB")
                product=SubProductAttribute.objects.get(pk=pk)
                productimages=SubProductAttributeImages.objects.filter(product_attribute__pk=pk)
                related_product=SubProductAttribute.objects.filter(product__slug=slug).exclude(pk=pk)
                product_qwantity  = ProductQuantity.objects.filter(product=product)
                context={
                'product':product,
                'image':productimages,
                'related':related_product,
                'product_qwantity':product_qwantity,
                }
                cache.set('pk', context)
       
