//Lical is 'Lihe-skite Calculator'.
//Since 2013
//Made by Daisy-Elise "Lihe" Leinhardt

#include <iostream>
#include <sstream>
#include <string>
#include <cctype>
#include <map>
#include <stdlib.h>

using namespace std;

enum Token_value
{
NAME, NUMBER, END, PLUS = '+', MINUS = '-', MUL = '*', DIV = '/', PRINT = ';', ASSIGN = '=', LP = '(', RP = ')', LPP = '{', RPP = '}', LPPP = '[', RPPP = ']', PRIME = 'P', EGG = '?'
};

map<string,long double> table;
Token_value curr_tok = PRINT;
long double term(bool);
long double expr(bool);
long double primary(bool);
void Prime_num();
inline void egg();
Token_value get_token();
double error(const string& s);
Token_value get_token();

int no_error;
long double num_value;
string string_value;
istream* input;

int main(int argc, char* argv[])
{
	system("clear");
	cout << "Hello, This Program is Lihe Calculator :)" << endl;

	switch(argc)
	{
	case 1:
	input = &cin;
	break;
	case 2:
	input = new istringstream(argv[1]);
	break;
	default:
	error("too many arguments");
	return 1;
	}
	
	table["pi"] = 3.1415926535897932384;
	table["e"] = 2.7182818284590452353;
	table["c"] = 299792.458;
	
	while(*input)
	{
	fst:
	get_token();
	if(curr_tok == END)
	break;
	if(curr_tok == PRINT)
	continue;
	if(curr_tok == PRIME)
	{
	get_token();
	Prime_num();
	goto fst;
	}
	if(curr_tok == EGG)
	{
	get_token();
	egg();
	goto fst;
	}
	cout << expr(false) << endl;
	}
	if(input != &cin)
	delete input;
	return no_error;
}

double error(const string& s)
{
	no_error++;
	cerr << "error: " << s << endl;
	return 1;
}

long double expr(bool get)
{
	long double output = term(get);
	for(;;)
	{
	switch(curr_tok)
	{
	case PLUS:
	output += term(true);
	break;
	case MINUS:
	output -= term(true);
	break;
	default:
	return output;
	}
	}
}

long double term(bool get)
{
	long double output = primary(get);
	for(;;)
	{
	switch(curr_tok)
	{
	case MUL:
	output *= primary(true);
	break;
	case DIV:
	if(long double d = primary(true))
	{
	output /= d;
	break;
	}
	return error("You can not divide by 0");
	default:
	return output;
	}
	}
}

long double primary(bool get)
{
	if(get)get_token();
	switch(curr_tok)
	{
	case NUMBER:
	{
	long double v = num_value;
	get_token();
	return v;
	}
	case NAME:
	{
	long double& v = table[string_value];
	if(get_token() == ASSIGN) v = expr(true);
	return v;
	}
	case MINUS:
	return -primary(true);
	case LP:
	{
	double e = expr(true);
	if(curr_tok != RP) return error("')' expected");
	get_token();
	return e;
	}
	case LPP:
	{
	double e = expr(true);
	if(curr_tok != RPP) return error("'}' expected");
	get_token();
	return e;
	}
	case LPPP:
	{
	double e = expr(true);
	if(curr_tok != RPPP) return error("']' expected");
	get_token();
	return e;
	}
	default:
	return error("primary expected");
	}
}

void Prime_num()
{
	long int output = (long int)num_value;
	long int count = 0;
	long int i = 1;
	if (output <= 1) goto notprm;
	for(;i <= output; i++)
	{
	if(output % i == 0)
	count++;
	}
	if(count >= 3)
	{
	notprm:
	cout << output << " is not a Prime Number." << endl;
	}
	else
	{
	cout << output << " is a Prime Number." << endl;
	}
}

inline void egg()
{
	cout << "Daisy, Daisy, Give me your answer do~" << endl;
}

Token_value get_token()
{
	char input;
	do
	{
	if(!cin.get(input))
	return curr_tok = END;
	}
	while(input != '\n' && isspace(input));
	switch(input)
	{
	case 0:
	return curr_tok = END;
	case ';':
	case '\n':
	return curr_tok = PRINT;
	case '+':
	case '-':
	case '*':
	case '/':
	case 'P':
	case '?':
	case '(':
	case ')':
	case '{':
	case '}':
	case '[':
	case ']':
	case '=':
	return curr_tok = Token_value(input);
	case'0':
	case'1':
	case'2':
	case'3':
	case'4':
	case'5':
	case'6':
	case'7':
	case'8':
	case'9':
	case'q':
	cin.putback(input);
	cin >> num_value;
	return curr_tok = NUMBER;
	default:
	if(isalpha(input))
	{
	string_value = input;
	while(cin.get(input) && isalnum(input))
	string_value.push_back(input);
	cin.putback(input);
	return curr_tok = NAME;
	}
	error("bad token");
	return curr_tok = PRINT;
	}
}
