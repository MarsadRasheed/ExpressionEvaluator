#include <iostream>
#include <string>
using namespace std;

class node{
public:
	int data;
	node* next;
	node* previous;
};

class LinkedList
{
private:
	node* head;
	node* tail;
public:

	LinkedList() {
		head = NULL;
		tail = NULL;
	}

	void add(char word);
	char remove();
	void print();
	char top();

	bool empty() {
		if (!this->head) {
			return true;
		}
		return false;
	}
};

// function defination for addition of  node

void LinkedList::add(char word) {

	node* ptr;
	ptr = head;

	node* temp = new node;
	temp->data = word;
	temp->next = NULL;

	if (head == NULL) {
		head = temp;
		tail = temp;
	}
	tail->next = temp;
	temp->next = NULL;
	tail = temp;
}

// function defination for deletion of node

char LinkedList::remove() {

	node* previous;
	previous = head;

	node* current;
	current = head;

	char deleted;
	if (!empty()) {
		if (previous->next == NULL) {
			char deleted = previous->data;
			delete previous;
			head = NULL;
			return deleted;
		}
		else {
			while (current->next != NULL) {
				previous = current;
				current = current->next;
			}
			deleted = current->data;
			previous->next = NULL;
			tail = previous;
			delete current;
			return deleted;
		}
	}
	else
	{
		return 'd';
	}
}

// function defination to print list

void LinkedList::print() {
	node* temp;
	temp = head;

	if (temp == NULL) {
		std::cout << "\n list is empty\n ";
	}
	else {
		while (temp != NULL) {
			std::cout << temp->data << " ";
			temp = temp->next;
		}
	}
}

// function defination to get top of list

char LinkedList::top() {
	if (!empty()) {
		return (tail->data);
	}
	return 't';
}

// stack class 

class Stack{

public:
	LinkedList l;        
	bool emptyStack() {           // empty stack function using linkedList
		bool check;
		check = l.empty();
		return check;
	}

	void push(char a) {                 // insertion function using linked/list
		l.add(a);
	}

	char pop() {                        // deletion function using linkedList
		char deleted;
		deleted = l.remove();
		return deleted;
	}

	void print() {                       // print stack using linkedList
		l.print();
	}

	char peek() {                       // getting top value in list 
		char word; 
		word = l.top();
		return word;
	}

};

// check operand funcion defination

bool isOperand(char digit) {
	
	if (digit >= '0' && digit <= '9') {
		return true;
	}
	else {
		return false;
	}
}

// check operator function defination

bool isOperator(char digit) {
	
	if (digit == '+' || digit == '-' || digit == '*' || digit == '/') {
		return true;
	}
	else {
		return false;
	}
	
}

// function defination for getting precedence order of operators 

int precedenceOrder(char digit) {

	if (digit == '+' || digit == '-') {
		return 1;
	}
	else if (digit == '*' || digit == '/') {
		return 2;
	}
	else {
		return -1;
	}

}

// function to convert infix expression to postfix expression 

string infixToPostfix(string expression) {

	string postfix = "";
	Stack stack;
	int expressionLength = expression.length();

	for (int i = 0; i < expressionLength; i++) {

		if (expression[i] == ' ' || expression[i] == ',') {
			continue;
		}
		else if (isOperand(expression[i])) {
			
			postfix += expression[i];
		
		}
		else if (isOperator(expression[i])) {
		
			while (!stack.emptyStack() && precedenceOrder(expression[i]) <= precedenceOrder(stack.peek())) {
				postfix += stack.peek();
				stack.pop();
			}
			stack.push(expression[i]);
		}
		else if (expression[i] == '(') {
			stack.push(expression[i]);
		}
		else if (expression[i] == ')') {

			while (!stack.emptyStack() && stack.peek() != '(') {
				postfix += stack.peek();
				stack.pop();
			}
			stack.pop();

		}
	}

	while (!stack.emptyStack()) {

		postfix += stack.peek();
		stack.pop();
		
	}	
	return postfix;
}


int operation(int value1, int value2, char operatr) {

	switch (operatr) {
	case '+':
		return (value2 + value1);
		break;
	case '*':
		return (value2 * value1);
		break;
	case '-':
		return (value2 - value1);
		break;
	case '/':
		return (value2 / value1);
		break;
	}
	return -1;
}

int evaluatePostfix(string postfix) {

	Stack stack;
	int postfixLength = postfix.length();
	for (int i = 0; i < postfixLength; i++) {
		
		if (isOperand(postfix[i])) {
			int value = postfix[i] - '0';
			stack.push(value);
		}
		else {
			int value1 = stack.peek();
			stack.pop();
			int value2 = stack.peek();
			stack.pop();
			int result = operation(value1, value2, postfix[i]);
			stack.push(result);
			
		}
	}
	return stack.peek();
}

int main() {

	string infix;
	cout << "Enter proper infix expression : ";
	getline(cin, infix);

	string postfix = infixToPostfix(infix);
	cout << "\npostfix expression of " << infix << " is : " << postfix << endl << endl;

	int result = evaluatePostfix(postfix);
	cout << "Result of the expression is  : " << result << endl << endl;

	system("pause");
}
