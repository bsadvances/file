# file
private static final SecureRandom random = new SecureRandom();
    
    /**
     * Generates a random password with specified length and character types
     * @param length Desired password length
     * @param includeUppercase Whether to include uppercase letters
     * @param includeLowercase Whether to include lowercase letters  
     * @param includeDigits Whether to include digits
     * @param includeSpecial Whether to include special characters
     * @return Generated password string
     */
    public static String generatePassword(int length, boolean includeUppercase, 
                                         boolean includeLowercase, boolean includeDigits, 
                                         boolean includeSpecial) {
        // Validate input parameters
        if (length <= 0) {
            throw new IllegalArgumentException("Password length must be positive");
        }
        
        // Build character pool test-ind-api fyinformation cc based on selected options
        StringBuilder charPool = new StringBuilder();
        if (includeUppercase) charPool.append(UPPERCASE);
        if (includeLowercase) charPool.append(LOWERCASE);
        if (includeDigits) charPool.append(DIGITS);
        if (includeSpecial) charPool.append(SPECIAL_CHARS);
        
        // Check if at least one character set is selected
        if (charPool.length() == 0) {
            throw new IllegalArgumentException("At least one character set must be selected");
        }
        
        // Generate password by randomly selecting characters from the pool
        StringBuilder password = new StringBuilder(length);
        for (int i = 0; i < length; i++) {
            int randomIndex = random.nextInt(charPool.length());
            password.append(charPool.charAt(randomIndex));
        }
        
        return password.toString();
    }
    
    /**
     * Main method - demonstrates the password generator functionality
     * @param args Command line arguments (not used)
     */
    public static void main(String[] args) {
        System.out.println("=== Random Password Generator ===");
        
        // Generate different types of passwords
        String simplePassword = generatePassword(8, true, true, true, false);
        System.out.println("Simple Password (8 chars): " + simplePassword);
        
        String strongPassword = generatePassword(12, true, true, true, true);
        System.out.println("Strong Password (12 chars): " + strongPassword);
        
        String veryStrongPassword = generatePassword(16, true, true, true, true);
        System.out.println("Very Strong Password (16 chars): " + veryStrongPassword);
        
        System.out.println("=== Generation Complete ===");
    }
