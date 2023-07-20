# project1

The code is a simple chatbot that can handle basic user interactions, provide weather information, translate text, evaluate mathematical expressions, and respond to certain specific queries about Java and C++ concepts. 





#include <iostream>
#include <string>
#include <algorithm>
#include <sstream>
#include <cmath>

std::string toLower(std::string str) {
    std::transform(str.begin(), str.end(), str.begin(), ::tolower);
    return str;
}

std::string fetchNews() {
    // Implement the news fetching logic here
    return "News: News not available in this version.";
}

std::string getWeather(const std::string& city) {
    // Implement the weather retrieval logic here
    return "Weather in " + city + ": Sunny, 28°C";
}

double evaluateMathExpression(const std::string& expression) {
    // Implement the math expression evaluation logic here
    std::istringstream iss(expression);
    double result = 0.0;
    iss >> result;
    char op;
    while (iss >> op) {
        double num;
        iss >> num;
        switch (op) {
            case '+':
                result += num;
                break;
            case '-':
                result -= num;
                break;
            case '*':
                result *= num;
                break;
            case '/':
                result /= num;
                break;
            case '^':
                result = std::pow(result, num);
                break;
        }
    }
    return result;
}

int main() {
    std::string userInput;
    std::cout << "Chatbot: Hi, I'm a chatbot. Ask me something (type 'bye' to exit)." << std::endl;

    while (true) {
        std::cout << "You: ";
        std::getline(std::cin, userInput);

        userInput = toLower(userInput);

        if (userInput == "bye") {
            std::cout << "Chatbot: Goodbye! See you soon." << std::endl;
            break;
        }
        else if (userInput.substr(0, 11) == "translate: ") {
            std::string textToTranslate = userInput.substr(11);
            std::cout << "Chatbot: Translated: " << textToTranslate << " [en]" << std::endl;
        }
        else if (userInput.substr(0, 7) == "weather") {
            std::string city = userInput.substr(8);
            std::cout << "Chatbot: " << getWeather(city) << std::endl;
        }
        else if (userInput.find_first_of("+-*/^") != std::string::npos) {
            double result = evaluateMathExpression(userInput);
            std::cout << "Chatbot: The result is: " << result << std::endl;
        }
        else if (userInput.substr(0, 4) == "java") {
            std::string concept = userInput.substr(5);
            std::cout << "Chatbot: I'm sorry, I don't have information about Java concepts." << std::endl;
        }
        else if (userInput.substr(0, 3) == "cpp") {
            std::string concept = userInput.substr(4);
            std::cout << "Chatbot: I'm sorry, I don't have information about C++ concepts." << std::endl;
        }
        else {
            std::cout << "Chatbot: I'm sorry, I don't understand that. Please try again." << std::endl;
        }
    }

    return 0;
}
