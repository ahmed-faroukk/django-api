<div class="markdown prose break-words dark:prose-invert dark"><p>To create a Flutter app that consumes a Django API, you will need to perform the following steps:</p><ol><li><p>Install Flutter and set up your development environment.</p></li><li><p>Create a new Flutter project using the following command:</p></li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-lua">flutter <span class="hljs-built_in">create</span> my_app
</code></div></div></pre><ol start="3"><li>Add the <code>http</code> and <code>json_serializable</code> dependencies to your <code>pubspec.yaml</code> file:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-yaml"><span class="hljs-attr">dependencies:</span>
  <span class="hljs-attr">flutter:</span>
    <span class="hljs-attr">sdk:</span> <span class="hljs-string">flutter</span>
  <span class="hljs-attr">http:</span> <span class="hljs-string">^0.12.0+2</span>
  <span class="hljs-attr">json_serializable:</span> <span class="hljs-string">^3.2.5</span>
</code></div></div></pre><ol start="4"><li>Run the following command to install the dependencies:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-csharp">flutter pub <span class="hljs-keyword">get</span>
</code></div></div></pre><ol start="5"><li>Create a model class for your products in the <code>lib/models</code> directory. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-dart">import 'package:json_annotation/json_annotation.dart';

part 'product.g.dart';

@JsonSerializable()
class Product {
  final int id;
  final String name;
  final double price;
  final int quantity;
  final String description;

  Product({this.id, this.name, this.price, this.quantity, this.description});

  factory Product.fromJson(Map&lt;String, dynamic&gt; json) =&gt; _$ProductFromJson(json);
  Map&lt;String, dynamic&gt; toJson() =&gt; _$ProductToJson(this);
}
</code></div></div></pre><ol start="6"><li>Run the following command to generate the serialization code for your model:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-rust">flutter <span class="hljs-keyword">pub</span> run build_runner build
</code></div></div></pre><ol start="7"><li>Create a service class for making HTTP requests to your Django API in the <code>lib/services</code> directory. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-dart">import 'package:http/http.dart' as http;
import 'dart:convert';

import 'package:my_app/models/product.dart';

class ProductService {
  static const endpoint = 'http://example.com/api/products';

  static Future&lt;List&lt;Product&gt;&gt; getProducts() async {
    try {
      final response = await http.get(endpoint);
      if (response.statusCode == 200) {
        List&lt;Product&gt; products = [];
        final data = json.decode(response.body);
        for (Map&lt;String, dynamic&gt; item in data) {
          products.add(Product.fromJson(item));
        }
        return products;
      }
    } catch (e) {
      print(e);
      return [];
    }
  }
}
</code></div></div></pre><ol start="8"><li>Use the <code>ProductService</code> class in your Flutter app to make HTTP requests to your Django API. For example:</li></ol><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-dart">import 'package:flutter/material.dart';
import 'package:my_app/services/product_service.dart';
import 'package:my_app/models/product.dart';

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() =&gt; _MyHomePageState();
}

class _MyHomePageState extends State&lt;MyHomePage
</code></div></div></pre></div>


<div class="markdown prose break-words dark:prose-invert dark"><p>To create the UI for a Flutter app that displays a list of supermarket products, you can use a <code>ListView</code> widget and a <code>Card</code> widget for each product.</p><p>Here is an example of how you might lay out the UI for the app:</p><pre><div class="bg-black mb-4 rounded-md"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4"><code class="!whitespace-pre-wrap hljs language-dart">import 'package:flutter/material.dart';
import 'package:my_app/models/product.dart';

class ProductList extends StatelessWidget {
  final List&lt;Product&gt; products;

  ProductList({this.products});

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: products.length,
      itemBuilder: (context, index) {
        return Card(
          child: Padding(
            padding: const EdgeInsets.all(8.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text(
                  products[index].name,
                  style: TextStyle(fontSize: 18),
                ),
                Text(
                  '${products[index].price} €',
                  style: TextStyle(color: Colors.grey),
                ),
                Text(
                  'Quantity: ${products[index].quantity}',
                  style: TextStyle(color: Colors.grey),
                ),
              ],
            ),
          ),
        );
      },
    );
  }
}
</code></div></div></pre><p>This code creates a <code>ListView</code> widget that displays a scrollable list of <code>Card</code> widgets, each of which displays the name, price, and quantity of a product.</p><p></p></div>
