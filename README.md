# DSACoding

class ConstructorError extends Error {
  constructor(message, details) {
    super(message); // Pass the error message to the parent Error class
    this.name = "ConstructorError"; // Set the name of the error type
    this.details = details; // Additional details about the error
    // Capture the stack trace for debugging purposes
    Error.captureStackTrace(this, ConstructorError);
  }
}

// Example usage:
class MyClass {
  constructor() {
    try {
      // Initialization code that might throw an error
      throw new ConstructorError("Initialization failed", { reason: "Missing parameters" });
    } catch (error) {
      console.error(error.name, error.message, error.details);
      // Rethrow the error if necessary
      throw error;
    }
  }
}

try {
  const instance = new MyClass();
} catch (error) {
  if (error instanceof ConstructorError) {
    console.error("Caught a constructor error:", error.message);
  } else {
    // Rethrow if not a ConstructorError
    throw error;
  }
}
