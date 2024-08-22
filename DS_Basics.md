```
// Day 1: Arrays and Strings in Java

// 1. Arrays
public class ArrayOperations {
    public static void main(String[] args) {
        // Declaring and initializing an array
        int[] numbers = {1, 2, 3, 4, 5};

        // Insertion (at the end)
        int[] newNumbers = new int[numbers.length + 1];
        System.arraycopy(numbers, 0, newNumbers, 0, numbers.length);
        newNumbers[newNumbers.length - 1] = 6;

        // Deletion (remove last element)
        int[] shorterNumbers = new int[numbers.length - 1];
        System.arraycopy(numbers, 0, shorterNumbers, 0, numbers.length - 1);

        // Traversal
        System.out.println("Array traversal:");
        for (int num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();

        // Searching
        int searchElement = 3;
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == searchElement) {
                System.out.println("Element " + searchElement + " found at index " + i);
                break;
            }
        }
    }
}

// 2. Strings
public class StringOperations {
    public static void main(String[] args) {
        String str = "Hello, World!";

        // Length
        System.out.println("Length: " + str.length());

        // Substring
        System.out.println("Substring: " + str.substring(0, 5));

        // Concatenation
        String newStr = str + " Welcome";
        System.out.println("Concatenated: " + newStr);

        // Replacement
        System.out.println("Replaced: " + str.replace("World", "Java"));

        // Splitting
        String[] parts = str.split(", ");
        System.out.println("Split parts: " + parts[0] + " and " + parts[1]);

        // Uppercase and Lowercase
        System.out.println("Uppercase: " + str.toUpperCase());
        System.out.println("Lowercase: " + str.toLowerCase());

        // Trim
        String spacedStr = "   Trim me   ";
        System.out.println("Trimmed: '" + spacedStr.trim() + "'");
    }
}

// Practice Exercises

// 1. Reverse an array
public static void reverseArray(int[] arr) {
    for (int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - 1 - i];
        arr[arr.length - 1 - i] = temp;
    }
}

// 2. Check if a string is a palindrome
public static boolean isPalindrome(String str) {
    str = str.toLowerCase().replaceAll("[^a-zA-Z0-9]", "");
    int left = 0;
    int right = str.length() - 1;
    while (left < right) {
        if (str.charAt(left) != str.charAt(right)) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// 3. Find the most frequent element in an array
public static int mostFrequent(int[] arr) {
    Map<Integer, Integer> frequencyMap = new HashMap<>();
    for (int num : arr) {
        frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
    }
    int maxFreq = 0;
    int mostFreqElement = arr[0];
    for (Map.Entry<Integer, Integer> entry : frequencyMap.entrySet()) {
        if (entry.getValue() > maxFreq) {
            maxFreq = entry.getValue();
            mostFreqElement = entry.getKey();
        }
    }
    return mostFreqElement;
}
```
