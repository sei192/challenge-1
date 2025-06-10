# challenge-1
python code 
class TrieNode:
    __slots__ = ['children', 'is_end_of_word']
    def __init__(self):
        self.children = [None] * 26
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
        self.has_any_word = False

    def insert(self, word: str) -> None:
        self.has_any_word = True
        if word == "":
            self.root.is_end_of_word = True
            return
        node = self.root
        for char in word:
            index = ord(char) - ord('a')
            if node.children[index] is None:
                node.children[index] = TrieNode()
            node = node.children[index]
        node.is_end_of_word = True

    def search(self, word: str) -> bool:
        if word == "":
            return self.root.is_end_of_word
        node = self.root
        for char in word:
            index = ord(char) - ord('a')
            if node.children[index] is None:
                return False
            node = node.children[index]
        return node.is_end_of_word

    def startsWith(self, prefix: str) -> bool:
        if prefix == "":
            return self.has_any_word
        node = self.root
        for char in prefix:
            index = ord(char) - ord('a')
            if node.children[index] is None:
                return False
            node = node.children[index]
        return True
