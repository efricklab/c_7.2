## ✅ **7.2 Lab – Reading and Writing Files in C**

**Environment**: GitHub Codespaces (with `gcc` pre-installed)

---

### **Introduction**

File I/O (Input/Output) in C allows programs to save and retrieve data using files stored on disk. In this lab, you'll learn how to write text to a file and then read it back using the standard C file-handling functions. This lab is divided into two parts:

* **Part 1**: Write and read a single record.
* **Part 2**: Use a loop to handle multiple records.

---

### **Objectives**

By the end of this lab, you will:

* Open and close files in C using `fopen()` and `fclose()`.
* Write data to a file using `fprintf()`.
* Read data from a file using `fgets()`.
* Use a loop to write multiple lines to a file.
* Display file contents in the terminal.

---

## 🧪 Part 1 – Single Record File I/O

---

### **Step 1: Open GitHub Codespaces**

1. Go to your GitHub repository.
2. Click **Code > Codespaces > Create codespace on main**.
3. Wait for your cloud-based editor to launch.

---

### **Step 2: Create a New C File**

1. In the **Explorer pane**, and open: `file_io.c`
2. Verify the following code:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    FILE *file;
    char name[50];
    int age;

    // Write to a file
    file = fopen("output.txt", "w");
    if (file == NULL) {
        printf("Error opening file for writing.\n");
        return 1;
    }

    printf("Enter your name: ");
    fgets(name, sizeof(name), stdin);
    name[strcspn(name, "\n")] = '\0'; // Remove newline

    printf("Enter your age: ");
    scanf("%d", &age);

    fprintf(file, "Name: %s\nAge: %d\n", name, age);
    fclose(file);
    printf("Data written to output.txt\n");

    // Read from the file
    file = fopen("output.txt", "r");
    if (file == NULL) {
        printf("Error opening file for reading.\n");
        return 1;
    }

    char line[100];
    printf("\nReading from file:\n");
    while (fgets(line, sizeof(line), file)) {
        printf("%s", line);
    }

    fclose(file);
    return 0;
}
```

---

### **Step 3: Compile the Program**

In the terminal:

```bash
gcc file_io.c -o file_io
```

---

### **Step 4: Run the Program**

```bash
./file_io
```

---

### **Step 5: Expected Output**

**Input Example:**

```
Enter your name: Alice
Enter your age: 30
```

**On-screen Output:**

```
Data written to output.txt

Reading from file:
Name: Alice
Age: 30
```

**File Content (`output.txt`):**

```
Name: Alice
Age: 30
```

---

## 🧪 Part 2 – Writing and Reading Multiple Records Using a Loop

---

### **Step 6: Update Your Code for Multiple Records**

Replace the contents of `file_io.c` with the following:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    FILE *file;
    int count;

    // Ask user how many records to write
    printf("How many records do you want to write? ");
    scanf("%d", &count);
    getchar(); // consume leftover newline

    // Open file for writing
    file = fopen("records.txt", "w");
    if (file == NULL) {
        printf("Error opening file for writing.\n");
        return 1;
    }

    // Loop to collect and write multiple records
    for (int i = 0; i < count; i++) {
        char name[50];
        int age;

        printf("Enter name for person %d: ", i + 1);
        fgets(name, sizeof(name), stdin);
        name[strcspn(name, "\n")] = '\0';

        printf("Enter age for person %d: ", i + 1);
        scanf("%d", &age);
        getchar(); // consume newline

        fprintf(file, "Name: %s\nAge: %d\n\n", name, age);
    }

    fclose(file);
    printf("\nAll records written to records.txt\n");

    // Open the file for reading
    file = fopen("records.txt", "r");
    if (file == NULL) {
        printf("Error opening file for reading.\n");
        return 1;
    }

    char line[100];
    printf("\nReading records from file:\n");
    while (fgets(line, sizeof(line), file)) {
        printf("%s", line);
    }

    fclose(file);
    return 0;
}
```

---

### **Step 7: Compile and Run**

```bash
gcc file_io.c -o file_io
./file_io
```

---

### **Step 8: Expected Output**

**Sample Input:**

```
How many records do you want to write? 2
Enter name for person 1: Alice
Enter age for person 1: 30
Enter name for person 2: Bob
Enter age for person 2: 25
```

**On-screen Output:**

```
All records written to records.txt

Reading records from file:
Name: Alice
Age: 30

Name: Bob
Age: 25
```

**File Content (`records.txt`):**

```
Name: Alice
Age: 30

Name: Bob
Age: 25
```

---

### **Summary**

In this lab, you learned how to:

* Use `fopen()` to create and open files for writing (`"w"`) and reading (`"r"`).
* Write structured text to a file using `fprintf()`.
* Use loops to collect and save multiple records.
* Read and display contents of a text file using `fgets()`.

File handling is essential in C for logging, saving user data, reading configuration files, and working with persistent data. You’re now ready to explore appending, parsing structured data, and working with binary files.
