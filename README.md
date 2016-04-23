# metod-Gausa

#pragma once

namespace методГаусса {

	using namespace System;
	using namespace System::ComponentModel;
	using namespace System::Collections;
	using namespace System::Windows::Forms;
	using namespace System::Data;
	using namespace System::Drawing;

	/// <summary>
	/// Summary for Form1
	/// </summary>
	public ref class Form1 : public System::Windows::Forms::Form
	{
	public:
		Form1(void)
		{
			InitializeComponent();
			//
			//TODO: Add the constructor code here
			//
		}

	protected:
		/// <summary>
		/// Clean up any resources being used.
		/// </summary>
		~Form1()
		{
			if (components)
			{
				delete components;
			}
		}
	private: System::Windows::Forms::TextBox^  textBox1;
	protected: 
	private: System::Windows::Forms::TextBox^  textBox2;
	private: System::Windows::Forms::TextBox^  textBox3;
	private: System::Windows::Forms::Label^  label1;
	private: System::Windows::Forms::Label^  label2;
	private: System::Windows::Forms::Label^  label3;
	private: System::Windows::Forms::Button^  button1;

	private:
		/// <summary>
		/// Required designer variable.
		/// </summary>
		System::ComponentModel::Container ^components;

#pragma region Windows Form Designer generated code
		/// <summary>
		/// Required method for Designer support - do not modify
		/// the contents of this method with the code editor.
		/// </summary>
		void InitializeComponent(void)
		{
			this->textBox1 = (gcnew System::Windows::Forms::TextBox());
			this->textBox2 = (gcnew System::Windows::Forms::TextBox());
			this->textBox3 = (gcnew System::Windows::Forms::TextBox());
			this->label1 = (gcnew System::Windows::Forms::Label());
			this->label2 = (gcnew System::Windows::Forms::Label());
			this->label3 = (gcnew System::Windows::Forms::Label());
			this->button1 = (gcnew System::Windows::Forms::Button());
			this->SuspendLayout();
			// 
			// textBox1
			// 
			this->textBox1->Location = System::Drawing::Point(24, 71);
			this->textBox1->Multiline = true;
			this->textBox1->Name = L"textBox1";
			this->textBox1->Size = System::Drawing::Size(100, 112);
			this->textBox1->TabIndex = 0;
			// 
			// textBox2
			// 
			this->textBox2->Location = System::Drawing::Point(140, 71);
			this->textBox2->Multiline = true;
			this->textBox2->Name = L"textBox2";
			this->textBox2->Size = System::Drawing::Size(51, 112);
			this->textBox2->TabIndex = 1;
			// 
			// textBox3
			// 
			this->textBox3->Location = System::Drawing::Point(237, 71);
			this->textBox3->Multiline = true;
			this->textBox3->Name = L"textBox3";
			this->textBox3->Size = System::Drawing::Size(100, 112);
			this->textBox3->TabIndex = 2;
			// 
			// label1
			// 
			this->label1->AutoSize = true;
			this->label1->Location = System::Drawing::Point(41, 55);
			this->label1->Name = L"label1";
			this->label1->Size = System::Drawing::Size(61, 13);
			this->label1->TabIndex = 3;
			this->label1->Text = L"Матрица А";
			// 
			// label2
			// 
			this->label2->AutoSize = true;
			this->label2->Location = System::Drawing::Point(137, 55);
			this->label2->Name = L"label2";
			this->label2->Size = System::Drawing::Size(61, 13);
			this->label2->TabIndex = 4;
			this->label2->Text = L"Матрица В";
			// 
			// label3
			// 
			this->label3->AutoSize = true;
			this->label3->Location = System::Drawing::Point(246, 54);
			this->label3->Name = L"label3";
			this->label3->Size = System::Drawing::Size(61, 13);
			this->label3->TabIndex = 5;
			this->label3->Text = L"Матрица Х";
			// 
			// button1
			// 
			this->button1->Location = System::Drawing::Point(128, 229);
			this->button1->Name = L"button1";
			this->button1->Size = System::Drawing::Size(75, 23);
			this->button1->TabIndex = 6;
			this->button1->Text = L"Подсчет";
			this->button1->UseVisualStyleBackColor = true;
			this->button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);
			// 
			// Form1
			// 
			this->AutoScaleDimensions = System::Drawing::SizeF(6, 13);
			this->AutoScaleMode = System::Windows::Forms::AutoScaleMode::Font;
			this->ClientSize = System::Drawing::Size(371, 262);
			this->Controls->Add(this->button1);
			this->Controls->Add(this->label3);
			this->Controls->Add(this->label2);
			this->Controls->Add(this->label1);
			this->Controls->Add(this->textBox3);
			this->Controls->Add(this->textBox2);
			this->Controls->Add(this->textBox1);
			this->Name = L"Form1";
			this->Text = L"Form1";
			this->ResumeLayout(false);
			this->PerformLayout();

		}
#pragma endregion
	private: System::Void button1_Click(System::Object^  sender, System::EventArgs^  e) {
				 String ^S = textBox1->Text;
				
				array<String^>^ SS = S->Split('\n');
				array<String^>^ line = SS[0]->Split(' ');

				int lines = SS->Length;	//количество строк
				int columns = line->Length;// количество столбцов
				double k = 0;	//К
				
				//выделение памяти под двумерный масив
				array<array<double>^>^ arrA = gcnew array<array<double>^>(lines); 
				for (int i = 0; i < lines; i++) 
				{
					arrA[i] = gcnew array<double>(columns);
				}
				// заполнение двумерного масива числами из TextBox1
				for(int index = 0; index < lines; index++)
				{
					array<String^>^ line = SS[index]->Split(' ');
					for(int indexLine = 0; indexLine < columns; indexLine++)
					{
						arrA[index][indexLine] = Convert::ToDouble(line[indexLine]);
					}
				}
				
				S = textBox2->Text;
				SS = S->Split('\n');
				lines = SS->Length;	// количество строк массива Б
				array<double>^ arrB = gcnew array<double>(lines); //выделение память под массив Б
				// заполнение массива Б
				for(int index = 0; index < lines; index++)
				{
					arrB[index] = Convert::ToDouble(SS[index]);
				}

				// прямой ход
				for(int index = 0; index < lines; index++)
				{
					if(arrA[index][index] != 1) // если элемента массива А[i][i] не равен 1
					{
						double koef = arrA[index][index]; // получаем этот элемент
						arrB[index] = arrB[index] / koef; // делим элемент Б[i] на элемент А[i][i]
						// делим все числа i-ой строки на элемент А[i][i]
						// получаем строку вида 1 х х | x, где х какие то новые числа после деления
						for(int indexTemp = index; indexTemp < columns; indexTemp++)
						{
							arrA[index][indexTemp] = arrA[index][indexTemp] / koef;
						}
					}
					// проходим в цикле по оставшимся строкам
					for(int indexLine = index+1; indexLine < columns; indexLine++)
					{
						k = arrA[indexLine][index] * (-1);	//умножаем на 
						if(0 != k)
						{
							arrB[index] = arrB[index] * k;	// домножить на К
							arrB[indexLine] += arrB[index];	// сложить с нижней строчкой
							arrB[index] = arrB[index] / k;	// востановить 

							for(int indexTemp = index; indexTemp < columns; indexTemp++)
							{
								arrA[index][indexTemp] = arrA[index][indexTemp] * k;
								arrA[indexLine][indexTemp] +=  arrA[index][indexTemp];
								arrA[index][indexTemp] = arrA[index][indexTemp] / k;
							}
						}
					}
				}
				// обратный ход
				for(int index = lines-1; index >= 0; index--)
				{
					// проходим в цикле по оставшимся строкам
					for(int indexLine = index-1; indexLine >= 0; indexLine--)
					{
						k = arrA[indexLine][index] * (-1);	 
						if(0 != k)
						{
							arrB[index] = arrB[index] * k;	
							arrB[indexLine] += arrB[index];	
							arrB[index] = arrB[index] / k;	

							for(int indexTemp = index; indexTemp < columns; indexTemp++)
							{
								arrA[index][indexTemp] = arrA[index][indexTemp] * k;
								arrA[indexLine][indexTemp] +=  arrA[index][indexTemp];
								arrA[index][indexTemp] = arrA[index][indexTemp] / k;
							}
						}
					}
				}
				
	
				textBox3->Text = L"";
				for(int index = 0; index < lines; index++)
				{
					if(index == lines-1)
						textBox3->Text = textBox3->Text + Convert::ToString((double)((int)(arrB[index]*100+0.5))/100.0);
					else
						textBox3->Text = textBox3->Text + Convert::ToString((double)((int)(arrB[index]*100+0.5))/100.0)+Environment::NewLine ;
				}

			 }
};
}
