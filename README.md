public class WordCounter {

    // Function to clean the input text by removing punctuation and converting to lowercase
    public static String cleanText(String text) {
        // Use regex to remove punctuation and convert the string to lowercase
        return text.toLowerCase().replaceAll("[^a-zA-Z\\s]", "");
    }

    // Function to check if a string is numeric
    public static boolean isNumeric(String str) {
        return str.matches("\\d+");
    }

    // Function to count word occurrences
    public static Map<String, Integer> countWords(String fileName) {
        Map<String, Integer> wordCount = new HashMap<>();

        try {
            // Read the file
            BufferedReader reader = new BufferedReader(new FileReader(fileName));
            String line;

            while ((line = reader.readLine()) != null) {
                // Clean the line by removing punctuation and converting to lowercase
                String cleanedLine = cleanText(line);
                // Split the line into words
                String[] words = cleanedLine.split("\\s+");

                // Count each word, skipping numeric words
                for (String word : words) {
                    if (!word.isEmpty() && !isNumeric(word)) {
                        wordCount.put(word, wordCount.getOrDefault(word, 0) + 1);
                    }
                }
            }
            reader.close();
        } catch (IOException e) {
            System.out.println("Error reading file: " + e.getMessage());
        }

        return wordCount;
    }

    // Function to print the word count in a formatted way
    public static void printWord
