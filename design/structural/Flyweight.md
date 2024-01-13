## Flyweight

Экономит память, разделяя общее состояние объектов между собой, вместо хранения одинаковых данных в каждом объекте.

Отделать неизменяемые повторяющиеся свойства.

```java
public class TreeFactory {
    private Map<String, TreeType> treeTypeMap = new HashMap<>();
    
    public Tree createTree(int x, int y, String name, Color color, Sprite sprite) {
        TreeType type = getTreeType(name, color, sprite);
        return new Tree(x, y, type);
    }

    private TreeType getTreeType(String name, Color color, Sprite sprite) {
        TreeType type = treeTypeMap.get(name);
        if (type == null) {
            type = new TreeType(name, color, sprite);
            treeTypeMap.put(name, type);
        }
        return type;
    }
}

public class TreeService {
    private TreeFactory treeFactory = new TreeFactory();
    private List<Tree> treeList = new ArrayList<>();

    public void createTree(int x, int y, String name, Color color, Sprite sprite) {
        Tree tree = treeFactory.createTree(x, y, name, color, sprite);
        treeList.add(tree);
    }
    
    public void drawAll() {
        for (Tree tree : treeList) {
            tree.draw();
        }
    }
}

@AllArgsConstructor
public class Tree {
    private int x;
    private int y;
    private TreeType type;

    public void draw() {
        // drawing logic
    }
}

public record TreeType(String name, Color color, Sprite sprite) {
}
```