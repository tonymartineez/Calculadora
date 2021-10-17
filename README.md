# Calculadora
// Calculadora4ADlg.cpp: archivo de implementación
//

#include "pch.h"
#include "framework.h"
#include "Calculadora4A.h"
#include "Calculadora4ADlg.h"
#include "afxdialogex.h"

#ifdef _DEBUG
#define new DEBUG_NEW
#endif


// Cuadro de diálogo CAboutDlg utilizado para el comando Acerca de

class CAboutDlg : public CDialogEx
{
public:
	CAboutDlg();

// Datos del cuadro de diálogo
#ifdef AFX_DESIGN_TIME
	enum { IDD = IDD_ABOUTBOX };
#endif

	protected:
	virtual void DoDataExchange(CDataExchange* pDX);    // Compatibilidad con DDX/DDV

// Implementación
protected:
	DECLARE_MESSAGE_MAP()
};

CAboutDlg::CAboutDlg() : CDialogEx(IDD_ABOUTBOX)
{
}

void CAboutDlg::DoDataExchange(CDataExchange* pDX)
{
	CDialogEx::DoDataExchange(pDX);
}

BEGIN_MESSAGE_MAP(CAboutDlg, CDialogEx)
END_MESSAGE_MAP()


// Cuadro de diálogo de CCalculadora4ADlg



CCalculadora4ADlg::CCalculadora4ADlg(CWnd* pParent /*= nullptr*/)
	: CDialogEx(IDD_CALCULADORA4A_DIALOG, pParent)
	, m_resultado(_T(""))
	, m_resultado_entero(0)
	, m_base(_T(""))
{
	m_hIcon = AfxGetApp()->LoadIcon(IDR_MAINFRAME);
}

void CCalculadora4ADlg::DoDataExchange(CDataExchange* pDX)
{
	CDialogEx::DoDataExchange(pDX);
	DDX_Text(pDX, IDC_RESULT_EDIT, m_resultado);
	DDX_Text(pDX, IDC_RESULT_STATIC, m_resultado_entero);
	DDX_CBString(pDX, IDC_BASE_COMBO, m_base);
}

BEGIN_MESSAGE_MAP(CCalculadora4ADlg, CDialogEx)
	ON_WM_SYSCOMMAND()
	ON_WM_PAINT()
	ON_WM_QUERYDRAGICON()
	ON_BN_CLICKED(IDC_0_BUTTON, &CCalculadora4ADlg::OnBnClicked0Button)
	ON_BN_CLICKED(IDC_1_BUTTON, &CCalculadora4ADlg::OnBnClicked1Button)
	ON_BN_CLICKED(IDC_2_BUTTON, &CCalculadora4ADlg::OnBnClicked2Button)
	ON_BN_CLICKED(IDC_3_BUTTON, &CCalculadora4ADlg::OnBnClicked3Button)
	ON_BN_CLICKED(IDC_4_BUTTON, &CCalculadora4ADlg::OnBnClicked4Button)
	ON_BN_CLICKED(IDC_5_BUTTON, &CCalculadora4ADlg::OnBnClicked5Button)
	ON_BN_CLICKED(IDC_6_BUTTON, &CCalculadora4ADlg::OnBnClicked6Button)
	ON_BN_CLICKED(IDC_7_BUTTON, &CCalculadora4ADlg::OnBnClicked7Button)
	ON_BN_CLICKED(IDC_8_BUTTON, &CCalculadora4ADlg::OnBnClicked8Button)
	ON_BN_CLICKED(IDC_9_BUTTON, &CCalculadora4ADlg::OnBnClicked9Button)
	ON_BN_CLICKED(IDC_SUMA_BUTTON, &CCalculadora4ADlg::OnBnClickedSumaButton)
	ON_BN_CLICKED(IDC_MUL_BUTTON, &CCalculadora4ADlg::OnBnClickedMulButton)
	ON_BN_CLICKED(IDC_RESTA_BUTTON, &CCalculadora4ADlg::OnBnClickedRestaButton)
	ON_BN_CLICKED(IDC_DIV_BUTTON, &CCalculadora4ADlg::OnBnClickedDivButton)
	ON_BN_CLICKED(IDC_IGUAL_BUTTON, &CCalculadora4ADlg::OnBnClickedIgualButton)
	ON_BN_CLICKED(IDC_CLEAR_BUTTON, &CCalculadora4ADlg::OnBnClickedClearButton)
END_MESSAGE_MAP()


// Controladores de mensajes de CCalculadora4ADlg

BOOL CCalculadora4ADlg::OnInitDialog()
{
	CDialogEx::OnInitDialog();

	// Agregar el elemento de menú "Acerca de..." al menú del sistema.

	// IDM_ABOUTBOX debe estar en el intervalo de comandos del sistema.
	ASSERT((IDM_ABOUTBOX & 0xFFF0) == IDM_ABOUTBOX);
	ASSERT(IDM_ABOUTBOX < 0xF000);

	CMenu* pSysMenu = GetSystemMenu(FALSE);
	if (pSysMenu != nullptr)
	{
		BOOL bNameValid;
		CString strAboutMenu;
		bNameValid = strAboutMenu.LoadString(IDS_ABOUTBOX);
		ASSERT(bNameValid);
		if (!strAboutMenu.IsEmpty())
		{
			pSysMenu->AppendMenu(MF_SEPARATOR);
			pSysMenu->AppendMenu(MF_STRING, IDM_ABOUTBOX, strAboutMenu);
		}
	}

	// Establecer el icono para este cuadro de diálogo.  El marco de trabajo realiza esta operación
	//  automáticamente cuando la ventana principal de la aplicación no es un cuadro de diálogo
	SetIcon(m_hIcon, TRUE);			// Establecer icono grande
	SetIcon(m_hIcon, FALSE);		// Establecer icono pequeño

	// TODO: agregar aquí inicialización adicional

	return TRUE;  // Devuelve TRUE  a menos que establezca el foco en un control
}

void CCalculadora4ADlg::OnSysCommand(UINT nID, LPARAM lParam)
{
	if ((nID & 0xFFF0) == IDM_ABOUTBOX)
	{
		CAboutDlg dlgAbout;
		dlgAbout.DoModal();
	}
	else
	{
		CDialogEx::OnSysCommand(nID, lParam);
	}
}

// Si agrega un botón Minimizar al cuadro de diálogo, necesitará el siguiente código
//  para dibujar el icono.  Para aplicaciones MFC que utilicen el modelo de documentos y vistas,
//  esta operación la realiza automáticamente el marco de trabajo.

void CCalculadora4ADlg::OnPaint()
{
	if (IsIconic())
	{
		CPaintDC dc(this); // Contexto de dispositivo para dibujo

		SendMessage(WM_ICONERASEBKGND, reinterpret_cast<WPARAM>(dc.GetSafeHdc()), 0);

		// Centrar icono en el rectángulo de cliente
		int cxIcon = GetSystemMetrics(SM_CXICON);
		int cyIcon = GetSystemMetrics(SM_CYICON);
		CRect rect;
		GetClientRect(&rect);
		int x = (rect.Width() - cxIcon + 1) / 2;
		int y = (rect.Height() - cyIcon + 1) / 2;

		// Dibujar el icono
		dc.DrawIcon(x, y, m_hIcon);
	}
	else
	{
		CDialogEx::OnPaint();
	}
}

// El sistema llama a esta función para obtener el cursor que se muestra mientras el usuario arrastra
//  la ventana minimizada.
HCURSOR CCalculadora4ADlg::OnQueryDragIcon()
{
	return static_cast<HCURSOR>(m_hIcon);
}

//area para declarar las variables globales numericas y no numericas
//que realizan las operaciones y muestran los resultados.
int conteo;     //almacena el # de click para un solo operador numerico
int op1;        //backup de el numero GENERADO
int op2;        //entero que almacena de forma local en cada funcion el resultado.
int codigo_de_operacion; // la suma = + es la opracion 1
						 //backup de variables temporales
int op1Suma;
int op2Suma;
int resultadoSuma;

int op1Mul;
int op2Mul;
int resultadoMul;

int op1Resta;
int op2Resta;
int resultadoResta;

int op1Div;
int op2Div;
int resultadoDiv;

void CCalculadora4ADlg::OnBnClicked0Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "0";
		m_resultado_entero = 0;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10;
		op1 = op2;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	UpdateData(FALSE);


}


void CCalculadora4ADlg::OnBnClicked1Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "1";
		m_resultado_entero = 1;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 1;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked2Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "2";
		m_resultado_entero = 2;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 2;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked3Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "3";
		m_resultado_entero = 3;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 3;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked4Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "4";
		m_resultado_entero = 4;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 4;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked5Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "5";
		m_resultado_entero = 5;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 5;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked6Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "6";
		m_resultado_entero = 6;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 6;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked7Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "7";
		m_resultado_entero = 7;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 7;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked8Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "8";
		m_resultado_entero = 8;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 8;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClicked9Button()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	if (conteo == 0) {
		m_resultado = "9";
		m_resultado_entero = 9;
		op1 = m_resultado_entero;
	}
	else {
		op2 = m_resultado_entero * 10; //op2 es el 1 convertido en decenas <<
		op1 = op2 + 9;
		m_resultado_entero = op1;
		//codigo para mandar a imprimir resultado en EDIT_BOX como CString
		CString MyCadena;
		MyCadena.Format(L"%d", op1);
		m_resultado = MyCadena;
	}
	conteo++;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedSumaButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	codigo_de_operacion = 1; // la suma = + es la operacion 1
	//backup de variables temporales
	op1Suma = op1;
	op2Suma = op2;
	resultadoSuma = m_resultado_entero;
	//borrado de variables
	conteo = 0; 
	op1 = 0;
	op2 = 0;
	m_resultado_entero = 0;

	CString MyCadena;
	MyCadena.Format(L"%d +", resultadoSuma);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedMulButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	codigo_de_operacion = 3; // la Mul = x es la operacion 3
	//backup de variables temporales
	op1Mul = op1;
	op2Mul = op2;
	resultadoMul = m_resultado_entero;
	//borrado de variables
	conteo = 0;
	op1 = 0;
	op2 = 0;
	m_resultado_entero = 0;

	CString MyCadena;
	MyCadena.Format(L"%d *", resultadoSuma);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedRestaButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	codigo_de_operacion = 2; // la Resta = - es la operacion 2
	//backup de variables temporales
	op1Resta = op1;
	op2Resta = op2;
	resultadoResta = m_resultado_entero;
	//borrado de variables
	conteo = 0;
	op1 = 0;
	op2 = 0;
	m_resultado_entero = 0;

	CString MyCadena;
	MyCadena.Format(L"%d -", resultadoSuma);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedDivButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	codigo_de_operacion = 4; // la Resta = - es la operacion 4
	//backup de variables temporales
	op1Div = op1;
	op2Div = op2;
	resultadoDiv = m_resultado_entero;
	//borrado de variables
	conteo = 0;
	op1 = 0;
	op2 = 0;
	m_resultado_entero = 0;

	CString MyCadena;
	MyCadena.Format(L"%d /", resultadoSuma);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedIgualButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	UpdateData(TRUE);
	switch (codigo_de_operacion)
	{
	case 1:
		m_resultado_entero = resultadoSuma + op1;
		break;
	case 2:
		m_resultado_entero = resultadoResta - op1;
		break;
	case 3:
		m_resultado_entero = resultadoMul * op1;
		break;
	case 4:
		m_resultado_entero = resultadoDiv / op1;
		break;

	default:
		break;
	}
	//madamos a imprimir a la cadena de edicion
	CString MyCadena;
	MyCadena.Format(L"= %d", m_resultado_entero);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}


void CCalculadora4ADlg::OnBnClickedClearButton()
{
	// TODO: Agregue aquí su código de controlador de notificación de control
	//borrado de variables 
	conteo = 0;
	op1 = 0;
	op2 = 0;
	m_resultado_entero = 0;
	resultadoSuma = 0;
	resultadoResta = 0;
	resultadoMul = 0;
	resultadoDiv = 0;

	CString MyCadena;
	MyCadena.Format(L"%d", m_resultado_entero);
	m_resultado = MyCadena;
	UpdateData(FALSE);
}
