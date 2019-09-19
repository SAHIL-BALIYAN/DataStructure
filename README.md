#include<iostream>
#include<string>
using namespace std;

struct Node
{
	int data;
	Node* next;
};

static Node* head;
class LinkedList
 {
	Node* head;
	Node* tail;

	Node* CreateNode(int data)
	{
		Node* temp = new Node();
		temp->data = data;
		temp->next = NULL;
		return temp;
	}

  public:
	LinkedList() :head(NULL), tail(NULL)
	{


	}


	void Append(int data)
	{
		Node* temp = CreateNode(data);
		if (head == NULL)
			head = temp;
		else
			tail->next = temp;
		tail = temp;

	}

	void Prepend(int data)
	{
		Node* temp = CreateNode(data);
		if (head == NULL)
			tail = temp;
		else
			temp->next = head;
		head = temp;
	}

	void Insert(int position, int data)
	{



		if (head == NULL)
			Append(data);

		else if (position == 1)
			Prepend(data);

		else
		{
			int i;
			Node* trav;
			for (i = 1, trav = head; trav != NULL && i < position - 1; i++, trav = trav->next);
			if (trav == NULL)
				Append(data);
			else
			{
				Node* temp = CreateNode(data);
				temp->next = trav->next;
				trav->next = temp;
			}
		}


	}


	void Insertsort(int data)
	{



		if (head == NULL)
			Append(data);



		//else if (data <= head->data)
			//Prepend(data);


		else
		{
			Node* trav = head;
			int flag = 1;
			while (trav != NULL)
			{
				if (data <= trav->data)
					Insert(flag, data);
				else
				{
					trav = trav->next;
					flag++;
				}
			}


		}


	}

		void Display()
		{
			for (Node* trav = head; trav != NULL; trav = trav->next)
			{
				cout << trav->data << "\t";
			}
			cout << endl;
		}


		~LinkedList()
		{
			while (head != NULL)
			{
				Node* temp = head;
				head = head->next;
				cout << "Releasing" << temp->data << endl;
				delete temp;
			}
			tail = NULL;
		}
	
};

	int main()
	{

		LinkedList l1;
		//int arr[] = { 10,5,7,3,25,15,30 };

		//for (auto val : arr) //c++11 range loops
		//{
			l1.Insertsort(10);
			l1.Insertsort(2);

		//}

		l1.Display();

		return 0;
	}
