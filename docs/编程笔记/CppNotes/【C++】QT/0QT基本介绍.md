# 0 QT 基本介绍

**Qt 是一个跨平台的 C++ 图形用户界面应用程序框架。**它为应用程序开发老提供建立艺术级图形界面所需的所有功能。它是完全面向对象的，很容易扩展，并且允许真正的组件编程。

QT是面向对象的框架。

QT SDK 软件开发包

QT 4.6之后 安装的 QT  SDK 既把 QT 安装好了，也把相关的环境安装好了。

在QT下载里面，x86-mingw530-....exe 后面的时间日期是编译器版本。 

编译流程：

```cpp
#include<QApplication>
#include<QLabel>
#include<QLineEdit>
#include<QPushButton>
#include<QHBoxLayout> //水平布局
#include<QVBoxLayout>//垂直布局
#include<QWidget> //窗口

int main(int argc, char *argv[])
{
    //打开一个窗口
    QApplication app(argc,argv);

    //提示信息控件
    QLabel *infoLabel = new QLabel;
    QLabel *openLabel = new QLabel;
    //编辑控件
    QLineEdit *cmdLineEdit = new QLineEdit;
    //按钮控件
    QPushButton *commitButton = new QPushButton;
    QPushButton *cancelButton = new QPushButton;
    QPushButton *browseButton = new QPushButton;


    infoLabel->setText("intput cmd:");
    openLabel->setText("open");
    commitButton->setText("commit");
    cancelButton->setText("cancel");
    browseButton->setText("browse");

    QHBoxLayout *cmdLayout = new QHBoxLayout;
    cmdLayout->addWidget(openLabel);
    cmdLayout->addWidget(cmdLineEdit);

    QHBoxLayout *buttonLayout = new QHBoxLayout;
    buttonLayout->addWidget(commitButton);
    buttonLayout->addWidget(cancelButton);
    buttonLayout->addWidget(browseButton);

    QVBoxLayout *mainLayout = new QVBoxLayout;
    mainLayout->addWidget(infoLabel);
    mainLayout->addLayout(cmdLayout);
    mainLayout->addLayout(buttonLayout);

    QWidget w;
    w.setLayout(mainLayout);
    w.show();


    //app.exec 程序永远执行
    return app.exec();
}
```

**<font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">（1）编写源文件</font>**

**<font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">（2）qmake –project</font>**

**<font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">（3）修改*.pro</font>**

**<font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">（4）qmake  *.pro</font>**

**<font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">（5）mingw32-make</font>**

# <font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">pro文件解释</font>
```cpp
//QT包含的模块
QT       += core gui
//大于4版本以上 包含 wigdet 模块
greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

//目标：生成的 .exe 程序名称
TARGET = FirstQT
//模板：应用程序模板 Application
TEMPLATE = app

DEFINES += QT_DEPRECATED_WARNINGS

CONFIG += c++11

//源文件，自动生成
SOURCES += \
        main.cpp \
        mywidget.cpp

//头文件
HEADERS += \
        mywidget.h

# Default rules for deployment.
qnx: target.path = /tmp/$${TARGET}/bin
else: unix:!android: target.path = /opt/$${TARGET}/bin
!isEmpty(target.path): INSTALLS += target

```

# 头文件解释
```cpp
#ifndef MYWIDGET_H
#define MYWIDGET_H

#include <QWidget> //包含头文件 QWidget 窗口类

class myWidget : public QWidget
{
    Q_OBJECT  //Q_QBJECT 宏，允许类中使用信号和槽的机制

public:
    myWidget(QWidget *parent = 0); //构造函数
    ~myWidget();  //析构
};

#endif // MYWIDGET_H

```

# <font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">Cpp文件</font>
```cpp
#include "mywidget.h"

// 命名规范
// 类名 首字母大写，单词和单词之间 首字母大写
// 函数名 变量名称 首字母小写 ，单词和单词之间首字母大写

myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
}

myWidget::~myWidget()
{

}

```

# <font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">按钮控件常用API</font>
```cpp
#include "mywidget.h"
#include<QPushButton> //按钮控件的头文件
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    //创建一个按钮
    QPushButton * btn = new QPushButton;
    //btn->show();//show以顶层的方式弹出窗口控件
    //让 btn 对象依赖在 myWidget 窗口中
    btn->setParent(this);
    
    //显示文本
    btn -> setText("第一个按钮");

    //创建第二个按钮
    QPushButton * btn2 = new QPushButton("第二个按钮",this);
    //移动 btn2
    btn2->move(100,100);
    //重置窗口的大小
    resize(600,400);
    //设置窗口的标题
    setWindowTitle("第一个窗口");
    //设置固定的窗口大小
    setFixedSize(600,400);
}

myWidget::~myWidget()
{

}
```

# <font style="color:rgb(51, 51, 51);background-color:rgb(254, 254, 254);">对象模型（对象树）</font>
```cpp
#include "DragSphereHandler.h"
#include<iostream>
#include <useNode>
#include <IViewer.h>
#include <MeshQuery.h>
using namespace std;
//#include <DebugView.h>
//#include <MathUtils.h>

#include <vector>

const static Color4f gDefaultColor = Color4f(0.7968f, 0.7152f, 0.4072f, 1.0f);	// 默认颜色

//初始化了mesh、render和node_三个成员变量,为小球的产生和拖动做准备，分别负责存储网格数据、渲染视图和节点数据。
DragSphereHandler::DragSphereHandler(SmartMesh mesh,IViewer* render):render_(render)
{
	mesh_ = mesh;	
	node_.reset(new Node);
	node_->SetName("DragSphereHandlerNode");
}


DragSphereHandler::~DragSphereHandler(void)
{
}


//在 DragSphereHandler 结束时,进行必要的清理工作,释放占用的资源,避免内存泄漏。
//释放了 node_、sphere_ 和 pickDrawable_ ,并设置实例无效
/*virtual*/ void DragSphereHandler::end(IViewer *viewer)
{
	if(viewer)
	{
		if(node_)
		{
			node_->clearAll();
			render_->getDocument()->rootNode()->removeChild(node_);
		}
		spheres.clear();
		pickDrawable_.reset();
		setValid(false);	
	}	
}

//入参：pos位置和半径radius。创建一个小球mesh,并把小球mesh移动到pos位置,最后返回创建的小球mesh。
SmartMesh DragSphereHandler::createSphere(Vec3f& pos,float radius /*= 1.f*/)
{
	shared_ptr<ObjectFilter> objectFilter(new ObjectFilter(ObjectFilter::OT_SPHERE));
	objectFilter->addPara("radius",radius);
	objectFilter->addPara("subdiv",1);
	shared_ptr<Mesh> mesh = objectFilter->createObject();

	mesh->SetName("sphere");

	// 设定mesh到pos
	Vec3f center = mesh->getMeshCenter();
	Matrixf mat;
	mat.SetTranslate(pos - center);
	processTrans(mesh, mat);
	mesh->setColor(gDefaultColor);
	mesh->notifyModified();
	mesh->dirtyMesh();
	return mesh;
}
//processTrans方法通过顶点坐标变换,实现了 mesh 的姿态变换
void DragSphereHandler::processTrans(shared_ptr<Mesh> mesh, const Matrixf& matTrans)
{
	int vertSize = mesh->vert.size();
	for(int i=0; i<vertSize; ++i)
	{
		TVertex* pVertex = mesh->getVertex(i);
		if(!pVertex)
			continue;
		pVertex->P() = matTrans * pVertex->P();
	}
	mesh->notifyModified();
	mesh->dirtyMesh();
}



bool DragSphereHandler::handle(QEvent *event, IViewer *viewer)
{
	if(!viewer)
	{
		return false;
	}

	switch(event->type())
	{
		case IEventHandler::PUSH:
		{
			QMouseEvent *e = TEvent::asMouseEvent(event);
			if(!e || e->button() != Qt::LeftButton)
				return false;

			Intersections intss;
			// 做射线，进行求交判断
			if(!viewer->computeIntersections(e->x(), e->y(), intss))
			{
				return false;
			}
			for(Intersections::iterator it = intss.begin();
				it != intss.end();
				++it)
			{
				// 光标在非Mesh区域
				if(!it->drawable)
				{
					pickDrawable_.reset();
					return false;
				}

				// 光标不在选中的小球中
				if(std::find(spheres.begin(), spheres.end(), it->drawable->asMesh()) == spheres.end())
				{
					qDebug("new small ball gene!");
					int i;
					//创建小球
					Vec3 hitPos = it->getWorldIntersectPoint(); // 定义hitPos
					//为每个小球自动设置"Sphere0"、"Sphere1"这样的数字名字, 方便小球的标识和管理
					std::string sphereName = "Sphere" + std::to_string(spheres.size());
					SmartMesh tempSphere = createSphere(hitPos);
					tempSphere->setName(sphereName.c_str());
					node_->addDrawable(tempSphere, true);
					render_->addChild(node_);
					spheres.push_back(tempSphere);//存入容器
					pickDrawable_ = spheres.back();
					break;
				}
				else
				{
					pickDrawable_ = it->drawable->asMesh();
					qDebug("pointer address:%x", pickDrawable_.get());
					break;
				}
			}
			break;
		}
		//MOVE,代码直接删除旧小球并创建新小球来"更新"位置
		case IEventHandler::MOVE:
		{
			QMouseEvent *e = TEvent::asMouseEvent(event);
			if(!e)
			{
				return false;
			}

			// 非左键按下返回
			if(e->buttons() != IEventHandler::LEFT_MOUSE_BUTTON)
			{
				break;
			}
			if(!pickDrawable_)
			{
				break;
			}
			Intersections intss;
			viewer->computeIntersections(e->x(), e->y(), intss);
			for(auto it = spheres.begin(); it != spheres.end(); ++it)
			{
				if((*it)->Name() == pickDrawable_->Name() && (*it)->Name() != "")// 如果当前选中的小球，如果当前小球名字不为空，那就是小球被选中了
				{
					(*it)->setColor(Color4f(1.0f, 0, 0, 1.0f));  // 把要移动的小球设置为红色
					Vec3 hitPoint;
					QString sphereName = (*it)->Name();
					for(Intersections::iterator iter = intss.begin();
						iter != intss.end();
						++iter)
					{
						if(iter->drawable->asMesh() == mesh_)
						{
							hitPoint = iter->getWorldIntersectPoint();
							node_->removeDrawable(*it);
							SmartMesh newSphere = createSphere(hitPoint);
							newSphere->SetName(sphereName);
							newSphere->setColor(Color4f(1.0f, 0, 0, 1.0f));
							node_->addDrawable(newSphere, true);
							*it = newSphere;
							break;
						}
					}
				}
			}
			break;
		
	}
		case IEventHandler::RELEASE:
		{
			QMouseEvent *e = TEvent::asMouseEvent(event);

			// 如果有小球被选中
			if(pickDrawable_)
			{
				// 遍历所有小球找到要移动的小球
				for(auto sphere : spheres)
				{
					if(sphere->Name() == pickDrawable_->Name() && sphere->Name() != "")
					{
						// 将球体颜色改为默认色
						sphere->setColor(gDefaultColor);
						break;
					}
				}
			}
			break;
		}


		case IEventHandler::KEYDOWN:
		{
			QKeyEvent *e = TEvent::asKeyEvent(event);

			if(e->key() == Qt::Key_Delete && pickDrawable_)
			{
				//遍历小球
				for(auto it = spheres.begin(); it != spheres.end(); ++it)
				{
					if((*it) == pickDrawable_)
					{
						node_->removeDrawable(*it);
						spheres.erase(it);
						pickDrawable_.reset(); // 这里删除后再清空pickDrawable_
						break;
					}
				}
			}
			break;
		}
	}
		viewer->render();
		return true;
}
```





> 更新: 2025-03-05 11:56:14  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/lpr9ggn2br8unudv>