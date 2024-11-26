
# **Inventory Framework Documentation**

---

## **Introduction**

The Unity Inventory Framework provides a versatile and extensible solution for creating inventory systems in Unity. Its design allows developers to quickly set up functional inventories while offering the flexibility to adapt to custom use cases. The framework supports a variety of inventory types, making it suitable for a wide range of games.

### **Key Features:**

- Predefined inventory types:
    - **List Inventory**: A straightforward collection of items.
    - **Equipment Inventory**: Ideal for RPGs or games with wearable gear.
    - **Grid Inventory**: Uniform item sizes (_free version_).
    - **Advanced Grid Inventory**: Supports items of varying sizes (_paid version only_).
    - **Puzzle Inventory**: A grid system for rotatable shapes (_paid version only_).
- Built on **UI Toolkit**: Offers advanced styling and layout capabilities while avoiding the overhead of GameObjects and prefabs. Learn more in the [UI Toolkit documentation](https://docs.unity3d.com/Manual/UIElements.html).
- Abstract yet powerful **item system** that minimizes setup while supporting diverse use cases.

This framework is targeted at **programmers**. It currently lacks designer-friendly features such as custom editors or Scriptable Objects, so some coding is required to implement custom functionality.

---

## **Getting Started**

To help you get familiar with the framework, the free version includes two demos: **Minimal** and **Basic**.

- The **Minimal Demo** demonstrates the simplest possible setup for a working inventory, perfect for understanding the fundamentals.
- The **Basic Demo** offers a more comprehensive example inspired by **Minecraft**, featuring:
    - A main inventory with equipment, a consumables hot-bar, and general storage.
    - A vendor system for buying and selling items.
    - A chest system for storing collections of items.
    - A crafting bench to create new items.
    - Stash functionality for persistent item storage.
    - Item dropping and destruction mechanics.

### **Installation**

Installing the framework is straightforward:

- **Free Version**: Available via Unity Package Manager or Git.
- **Paid Version**: Downloadable from the Unity Asset Store.

The package has **no external dependencies**, ensuring smooth integration into your existing projects.

---

## **Core Concepts**

The framework is built around several key concepts that define its structure and behavior. Understanding these will help you make the most of its features.

### **Item**

An **Item** represents an individual object in the inventory system. It is highly flexible and comprises two main components:

- **Base**: Contains fixed properties like ID, name, and icon path.
- **Data**: Holds dynamic properties such as quantity or stackability.

This separation ensures adaptability, allowing items to fit various gameplay scenarios with minimal effort.

### **Slot**

A **Slot** is a container that can either hold an **Item** or remain empty. Slots can enforce **restrictions**, such as allowing only specific types of items.  
Specialized slots include:

- **List Slots**: Index-based storage.
- **Equipment Slots**: Named slots for wearable items.
- **Grid Slots** (_paid version only_): Position-based storage.

### **Inventory**

An **Inventory** manages a collection of **Slots**. Each inventory type comes with its own behavior and can enforce restrictions on acceptable items. Specialized inventory types include:

- **List Inventory**.
- **Equipment Inventory**.
- **Grid Inventory** (_paid version only_).

Inventories also notify subscribers of state changes through an **Observable** mechanism, making it easy to update views or other systems.

### **Event Bus and Events**

The framework uses an **Event Bus** to decouple its components. Events are data containers describing actions, such as picking up an item. For example, an "ItemPicked" event might include:

- The item itself.
- The source inventory and slot.

### **Store**

Inspired by **Redux**, the **Store** serves as the central hub for managing system state. It listens for events and performs necessary state updates. All changes to the system state flow through the Store, ensuring consistency and predictability.

---

## **Technical Details**

The framework takes a **functional programming approach**, emphasizing immutability and separation of concerns.

- **Records** are used to model data, offering concise syntax and value-like behavior.
- Behavior is implemented via **extension methods** to keep the data structures clean and focused.
- **Factories** ensure proper input validation when creating new instances.
- The **null object pattern** is employed to represent the absence of an object (e.g., a slot containing "No-Item").

This design minimizes side effects, making the system more predictable and easier to debug.

---

## **UI Toolkit Integration**

The framework leverages **UI Toolkit** for rendering inventory views. While it avoids **UXML** for ease of development, it provides a declarative way to define elements, their data, and their styles in C#.

### **Highlights**:

- Fully utilizes **C# and USS** for flexibility.
- Web-inspired nomenclature, such as:
    - **DOM**: Utility functions for managing elements.
    - **DIV**: A shorthand alias for `VisualElement`.
- While you can’t view included visual elements in Unity's UI Builder, you can use it to design custom components.

This approach ensures a seamless development workflow while maintaining compatibility with Unity’s evolving UI system.

---

## **How to Use the Framework**

1. **Set up an inventory**: Start by modifying or cloning one of the provided demos. Cloning ensures you don’t lose your changes when updating the package.
2. **Add new items**:
    - Define a new item base in the `AllBases` dictionary.
    - Use the `ItemFactory.Create` function to create the item.
    - Add the item to an inventory using `AddItem` or `SetItems` in the _Store_'s `Reset` method.
3. **Reference examples**: Use the provided samples for guidance on extending functionality.

---

## **Troubleshooting**

### **Common Issues**

1. **UI Toolkit Debugging**: Use the [UI Toolkit Debugger](https://docs.unity3d.com/Manual/UIElementsDebugger.html) to inspect element styles and classes.
2. **CSS Cascade Problems**: Check for unintended style propagation affecting your UI.

### **Debugging Tools**

- Use the included editor windows to view the raw state of the system. These tools help identify whether issues originate from the data layer or the view layer.

### **Need Help?**

Join our **Discord server** to ask questions and get support from the community.

---

## **Roadmap**

- **Paid Features**:
    - Advanced grid inventory with varying item sizes.
    - Puzzle inventory.
- **Persistence**: Save/load functionality using JSON and/or CSV.
- **Designer Tools**: Investigating support for Scriptable Objects and custom editors.

---
