# trie_router

A Trie-based route parser.

## Usage

```dart
import 'package:trie_router/trie_router.dart';
import 'package:path/path.dart' as path;

typedef RouteHandler = void Function(Map<String, String> parameters);

TrieRouter router = TrieRouter<RouteHandler>();

void main() {
  // Add routes
  addRoute('', (_) => print('Displaying home page'));
  addRoute('users/:id', (params) => print('Displaying user ${params[":id"]}'));
  addRoute('users/:id/settings',
      (params) => print('Displaying settings for user ${params[":id"]}'));

  // Handle routes
  handlePath('');
  handlePath('users/123');
  handlePath('users/123/settings');
}

void addRoute(String s, RouteHandler handler) {
  router.add(path.split(s), handler);
}

void handlePath(String s) {
  var element = router.get(path.split(s));
  element.value(element.parameters);
}
```
