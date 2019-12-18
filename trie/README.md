# Trie

如何见trie

```text
for word in words:
    p = root
    for w in word:
        
        i = ord(w)-ord('a')
        print(i)
        if p.next[i] is None:
            p.next[i] = TrieNode()
        p = p.next[i]
    p.word = word

```

```text
    def build(self,words):
        
        for word in words:
            root = self.root
            for c in word:
                if c not in root:
                    root[c] = {}
                root = root[c]
         
            root['#'] = word
```

search\_prefix:

```text
    def search_prefix(self,node,prefix,candidates):
        if '#' in node:
            candidates.append(node['#'])
            return
        for letter in prefix:
            if letter not in node:
                return
            node = node[letter]
       
        for letter in node:
            #print(letter,node[letter])
            self.search_prefix(node[letter],'',candidates)
     
```

