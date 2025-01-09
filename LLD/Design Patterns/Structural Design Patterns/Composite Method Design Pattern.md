# Composite Method Pattern - File System Example

## Overview
The **Composite Method pattern** is a structural design pattern that allows you to compose objects into tree-like structures to represent part-whole hierarchies. It enables treating individual objects and compositions of objects uniformly.

This example demonstrates the Composite Method pattern applied to a file system, where both files and directories are treated as components of a hierarchical structure.

---

## Use Case: File System
The example implements a file system where:
- **File**: Represents individual files (leaf nodes).
- **Directory**: Represents directories that can contain files or other directories (composite nodes).

Both files and directories share a common interface, enabling operations like:
- Displaying details of all components.
- Calculating the total size of files and directories.

---

## Structure
### Classes and Interfaces:
1. **`FileSystemComponent`** (Interface):
   - Represents the common interface for both files and directories.
   - Methods:
     - `void showDetails()`: Displays details of the component.
     - `long getSize()`: Returns the size of the component.

2. **`File`** (Leaf):
   - Implements the `FileSystemComponent` interface.
   - Represents individual files.
   - Attributes:
     - `name`: Name of the file.
     - `size`: Size of the file.

3. **`Directory`** (Composite):
   - Implements the `FileSystemComponent` interface.
   - Represents directories that can contain files or other directories.
   - Attributes:
     - `name`: Name of the directory.
     - `components`: A list of `FileSystemComponent` (files and directories).

4. **`Main`** (Client):
   - Creates files and directories.
   - Adds files and directories to the tree structure.
   - Performs operations like displaying details and calculating total size.

---

## Code Example
Here is the implementation in Java:

```java
// Component
interface FileSystemComponent {
    void showDetails();
    long getSize();
}

// Leaf
class File implements FileSystemComponent {
    private String name;
    private long size;

    public File(String name, long size) {
        this.name = name;
        this.size = size;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name + ", Size: " + size + " KB");
    }

    @Override
    public long getSize() {
        return size;
    }
}

// Composite
class Directory implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> components = new ArrayList<>();

    public Directory(String name) {
        this.name = name;
    }

    public void addComponent(FileSystemComponent component) {
        components.add(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Directory: " + name);
        for (FileSystemComponent component : components) {
            component.showDetails();
        }
    }

    @Override
    public long getSize() {
        long totalSize = 0;
        for (FileSystemComponent component : components) {
            totalSize += component.getSize();
        }
        return totalSize;
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        FileSystemComponent file1 = new File("file1.txt", 120);
        FileSystemComponent file2 = new File("file2.txt", 200);

        FileSystemComponent directory1 = new Directory("Documents");
        ((Directory) directory1).addComponent(file1);
        ((Directory) directory1).addComponent(file2);

        FileSystemComponent file3 = new File("file3.txt", 150);
        FileSystemComponent directory2 = new Directory("Images");
        ((Directory) directory2).addComponent(file3);

        FileSystemComponent rootDirectory = new Directory("Root");
        ((Directory) rootDirectory).addComponent(directory1);
        ((Directory) rootDirectory).addComponent(directory2);

        // Show details of the entire file system
        rootDirectory.showDetails();

        // Get total size of all components in the root directory
        System.out.println("Total Size: " + rootDirectory.getSize() + " KB");
    }
}
```

---

## Output
When running the above code, the output will look like this:

```
Directory: Root
Directory: Documents
File: file1.txt, Size: 120 KB
File: file2.txt, Size: 200 KB
Directory: Images
File: file3.txt, Size: 150 KB
Total Size: 470 KB
```

---

## Pros and Cons of the Composite Method Pattern

### Pros:
1. **Simplifies client code**: Treats individual objects and composites uniformly.
2. **Flexible**: Allows for the dynamic addition of components.
3. **Easier maintenance**: Modifications to the structure are straightforward.

### Cons:
1. **Complexity**: Can become overly complicated for simple hierarchies.
2. **Operations**: Some operations might be hard to implement uniformly across components.

---

## Real-World Analogy
The Composite Method pattern is analogous to a **folder system on a computer**:
- Files are individual objects (leaf nodes).
- Folders are composite objects that can contain files or other folders.
- Both files and folders support operations like opening or deleting.

---

## Use Cases
1. **File systems**: Managing files and folders.
2. **Organizational structures**: Employees and teams.
3. **UI components**: Buttons, panels, and composite views.

---

## Conclusion
The Composite Method pattern is ideal for managing part-whole hierarchies where individual objects and groups of objects need to be treated in a uniform way. This file system example showcases its application and demonstrates how it simplifies working with hierarchical structures in Java.

