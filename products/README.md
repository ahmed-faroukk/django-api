<div class="markdown prose break-words dark:prose-invert dark"><p> you will need to perform the following steps:</p><ol><li>Create a new Django project and app:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-bash">django-admin startproject supermarket
<span class="hljs-built_in">cd</span> supermarket
python manage.py startapp products
</code></div></div></pre><ol start="2"><li>Define the models for your products in the <code>products/models.py</code> file. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-python"><span class="hljs-keyword">from</span> django.db <span class="hljs-keyword">import</span> models

<span class="hljs-keyword">class</span> <span class="hljs-title class_">Product</span>(models.Model):
    name = models.CharField(max_length=<span class="hljs-number">255</span>)
    price = models.DecimalField(max_digits=<span class="hljs-number">5</span>, decimal_places=<span class="hljs-number">2</span>)
    quantity = models.PositiveIntegerField()
    description = models.TextField(blank=<span class="hljs-literal">True</span>)
</code></div></div></pre><ol start="3"><li>Run the following command to create the database tables for your models:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs">python manage.py makemigrations
python manage.py migrate
</code></div></div></pre><ol start="4"><li>Use Django's built-in Serialization framework to create a serializer class for your <code>Product</code> model in the <code>products/serializers.py</code> file. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-python"><span class="hljs-keyword">from</span> rest_framework <span class="hljs-keyword">import</span> serializers
<span class="hljs-keyword">from</span> .models <span class="hljs-keyword">import</span> Product

<span class="hljs-keyword">class</span> <span class="hljs-title class_">ProductSerializer</span>(serializers.ModelSerializer):
    <span class="hljs-keyword">class</span> <span class="hljs-title class_">Meta</span>:
        model = Product
        fields = <span class="hljs-string">'__all__'</span>
</code></div></div></pre><ol start="5"><li>Create views for the API in the <code>products/views.py</code> file. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-python"><span class="hljs-keyword">from</span> django.shortcuts <span class="hljs-keyword">import</span> get_object_or_404
<span class="hljs-keyword">from</span> rest_framework <span class="hljs-keyword">import</span> generics
<span class="hljs-keyword">from</span> .models <span class="hljs-keyword">import</span> Product
<span class="hljs-keyword">from</span> .serializers <span class="hljs-keyword">import</span> ProductSerializer

<span class="hljs-keyword">class</span> <span class="hljs-title class_">ProductList</span>(generics.ListCreateAPIView):
    queryset = Product.objects.<span class="hljs-built_in">all</span>()
    serializer_class = ProductSerializer

<span class="hljs-keyword">class</span> <span class="hljs-title class_">ProductDetail</span>(generics.RetrieveUpdateDestroyAPIView):
    queryset = Product.objects.<span class="hljs-built_in">all</span>()
    serializer_class = ProductSerializer
</code></div></div></pre><ol start="6"><li>Define the URLs for your API in the <code>supermarket/urls.py</code> file. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-python"><span class="hljs-keyword">from</span> django.contrib <span class="hljs-keyword">import</span> admin
<span class="hljs-keyword">from</span> django.urls <span class="hljs-keyword">import</span> include, path

urlpatterns = [
    path(<span class="hljs-string">'admin/'</span>, admin.site.urls),
    path(<span class="hljs-string">'api/products/'</span>, include(<span class="hljs-string">'products.urls'</span>)),
]
</code></div></div></pre><ol start="7"><li>Create a <code>products/urls.py</code> file to define the URLs for your product views. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-python"><span class="hljs-keyword">from</span> django.urls <span class="hljs-keyword">import</span> path
<span class="hljs-keyword">from</span> . <span class="hljs-keyword">import</span> views

urlpatterns = [
    path(<span class="hljs-string">''</span>, views.ProductList.as_view(), name=<span class="hljs-string">'product_list'</span>),
    path(<span class="hljs-string">'&lt;int:pk&gt;/'</span>, views.ProductDetail.as_view(), name=<span class="hljs-string">'product_detail'</span>),
]
</code></div></div></pre><ol start="8"><li><p>Test your API using Django's built-in development server and the Django Rest Framework browsable API.</p></li><li><p>To deploy your API to a free host, you can use a platform like PythonAnywhere or Heroku. Both of these platforms offer free tiers that allow you to host small Django applications.</p></li></ol><p></p></div>
