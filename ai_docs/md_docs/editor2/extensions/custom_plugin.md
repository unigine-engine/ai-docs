# Creating Your First Editor Plugin


This article describes how to create an Editor plugin and get the first impression of what a plugin consists of and what its general structure is.


> **Warning:** This feature is an experimental one and is not recommended for production use.


UnigineEditor is an application written entirely in C++ relying a lot on the Qt6 framework infrastructure. So, in order to extend its functionality not only C++ programming skills are required, but you should also be familiar with the Qt6 framework, and CMake build system (especially if you use Linux).


> **Notice:** *Qt Framework* version **6.5.3** is required to develop plugins for UnigineEditor. More information on setting up development environment for this purpose is available in [this article](../../editor2/extensions/environment.md).


### See Also


- [Extending Editor Functionality](../../editor2/extensions/index.md) article for more information on UnigineEditor's Plugin System and extensions.
- *[Editor API Reference](/api/editor/index.md)* for more information on all available classes.
- [Creating C++ Plugin](../../code/cpp/plugin.md#naming) article for information on the naming convention and plugin files location.


## Plugin Templates


For your convenience there are three project templates (**[Engine GUI Window](#engineguiwindow_plugin)**, **[Assets](#assets_plugin)**, and **[Materials](#materials_plugin)**) that you can use as a basis to create your own plugin. Below you'll find a brief description of each template.


### Materials Plugin


This plugin template implements the basic functionality of the Editor's *Materials Hierarchy* window (see the picture below).


> **Notice:** Only *Release* version of this plugin template is available.


![Materials Plugin](materialspl.png)

*Materials Plugin*


Basically the plugin's architecture looks as follows:


![Materials Plugin Architecture](materialsuml.png)

*Materials Plugin*


The *MaterialsPlugin* class is an initialization point and complete representation of the plugin.  It creates necessary data model and via the base interface associates it with the widget, which displays the hierarchy. The model directly interacts with the *Materials Manager* and transforms information on materials to the required structure.


The plugin interacts with Engine Materials System and Editor's external subsystems:


- Adds a widget to *[WindowManager](/api/editor/class_unigine_editor_1_1_window_manager.md)*.
- Adds a new item to the main menu bar.
- Updates the state of materials widget when the global selection is changed.
- Updates the global selection when the local selection is changed by sending a *[SelectionAction](/api/editor/class_unigine_editor_1_1_selection_action.md)* to the Undo stack.


### Engine Gui Window Plugin


This plugin template implements a simple dockable window of the UnigineEditor with a simple GUI example that displays the current selection in the *World Nodes* hierarchy window, and enables you to assign a C++ component to selected nodes (see the picture below).


![Engine Gui Window Plugin](engineguiwindow_plugin.png)

*Engine Gui WindowPlugin*


The *EngineGuiWindowPlugin* class is an initialization point and complete representation of the plugin.


The plugin interacts with Editor's external subsystems:


- Adds a widget to *[WindowManager](/api/editor/class_unigine_editor_1_1_window_manager.md)*.
- Adds a new item to the main menu bar.
- Interacts with Editor's *Drag&Drop* System and enables dragging and dropping files within the window area, prints their names to the Console.
- Monitors current window focus state.
- Updates the global selection when the local selection is changed by sending a *[SelectionAction](/api/editor/class_unigine_editor_1_1_selection_action.md)* to the Undo stack, when a node is selected and the *Add components to selection!* button is clicked.


And the following Engine subsystems:


- C++ Component System
- GUI System
- Input System


### Assets Plugin


This is a sample plugin demonstrating implementation of basic asset management operations using the *[AssetManager](/api/editor/class_unigine_editor_1_1_asset_manager.md)* class (see the picture below).


![Assets Plugin](assetspl.png)

*AssetsPlugin*


The *AssetsPlugin* class is an initialization point and complete representation of the plugin.


The plugin interacts with Editor's external subsystems:


- Adds a widget to *[WindowManager](/api/editor/class_unigine_editor_1_1_window_manager.md)*.
- Adds a new item to the main menu bar.
- Interacts with Editor's *[AssetManager](/api/editor/class_unigine_editor_1_1_asset_manager.md)* class, displays messages in the label element.
- Monitors current selection state.
- Updates the global selection after importing assets.


And the following Engine subsystems:


- File System
- GUI System
- Input System


For more information about the *Assets* Plugin please refer to [this article](../../editor2/extensions/manage_assets.md).


## Using Plugin Template


To start developing your plugin for UnigineEditor perform the following actions:


1. Check the **Editor Plugin Template** option when [creating a new project](../../sdk/projects/index_cpp.md#creation) in *SDK Browser* (or choose *Other Actions -> Configure Project* if you want to use your new Editor plugin in an existing project). ![Adding a plugin template](create_plugin.png)
2. Click *Create New Project* (or *Update Configuration* if you're adding a template to an existing project).


After clicking the *Create New Project / Update Configuration* button, a set of projects for the Editor plugins will be added to your UNIGINE project's `source` folder and all necessary files will be added to these folders depending on your operating system and *API + IDE* selection in project settings:


- **Windows OS: C++ (Qt-based / CMake) or UnigineScript** � *CMake* will be used to build your plugin.
- **Windows OS: C# (.NET) or C++ (Visual Studio)** � a `.vcxproj` project will be created and *Visual Studio 2022* will be used to build your plugin.
- **Linux** � *CMake* will be used to build your plugin regardless of project configuration.


You can open this project in your IDE, build it, and give it a test drive right in the Editor as the project is pre-configured to launch with the UnigineEditor.


## Plugin's Logic Implementation


Now let's have a quick look at the implementation of our plugin template's logic. As an example let's choose the **Materials** plugin.


### Plugin Class


The files *MaterialsPlugin.h* and *MaterialsPlugin.cpp* define the implementation of our plugin. Let's highlight some important points here.


#### Header File


The header file `MaterialsPlugin.h` defines the interface of the plugin class.


```cpp
namespace Materials
{


```


The plugin is defined in a *Materials* namespace, which conforms to the coding rules for namespacing in sources.


```cpp
class MaterialsPlugin : public QObject, public ::UnigineEditor::Plugin
{
	Q_OBJECT
	Q_DISABLE_COPY(MaterialsPlugin)
	Q_PLUGIN_METADATA(IID UNIGINE_EDITOR_PLUGIN_IID FILE "MaterialsPlugin.json")
	Q_INTERFACES(UnigineEditor::Plugin)


```


All Editor plugins must be derived from *[Editor::Plugin](/api/editor/class_unigine_editor_1_1_plugin.md)* class and are *QObjects*. The `Q_PLUGIN_METADATA` macro is necessary to create a valid Editor plugin. The IID given in the macro must be **UNIGINE_EDITOR_PLUGIN_IID**, to identify it as an Editor plugin, and *FILE* must point to the plugin's meta data file as described in [Plugin Meta Data](../../editor2/extensions/index.md#plugin_meta).


```cpp
bool init() override;
void shutdown() override;


```


The base class defines basic functions that are called during the [life cycle](../../editor2/extensions/index.md#plugin_lifecycle) of a plugin (on initialization and shutdown), which are here implemented for your new plugin.


Our plugin has three additional custom slots, that are used show the view, set global selection and update the local one when the global is changed.


```cpp
public slots:
	void showView();
	void setGlobalSelection(const QModelIndexList &indexes);
	void globalSelectionChanged();


```


<details>
<summary>MaterialsPlugin.h | Close</summary>

**MaterialsPlugin.h**


```cpp
#pragma once

#include <editor/UniginePlugin.h>

#include <QObject>
#include <QModelIndex>

namespace Materials
{

class MaterialsModel;
class MaterialsView;
}

class QAction;

namespace Materials
{
class MaterialsPlugin : public QObject, public ::UnigineEditor::Plugin
{
	Q_OBJECT
	Q_DISABLE_COPY(MaterialsPlugin)
	Q_PLUGIN_METADATA(IID UNIGINE_EDITOR_PLUGIN_IID FILE "MaterialsPlugin.json")
	Q_INTERFACES(UnigineEditor::Plugin)
public:
	MaterialsPlugin() = default;
	~MaterialsPlugin() override;
	bool init() override;
	void shutdown() override;
public slots:
	void showView();
	void setGlobalSelection(const QModelIndexList &indexes);
	void globalSelectionChanged();
private:
	MaterialsModel *model_{nullptr};
	MaterialsView *view_{nullptr};
	QAction *action_{nullptr};
};

} // namespace Materials

```

</details>


#### Implementation File


This file contains the actual implementation of our plugin and its logic. For more information about implementing the plugin interface, see the *[**Editor::Plugin**](/api/editor/class_unigine_editor_1_1_plugin.md)* API documentation and [Plugin Life Cycle](../../editor2/extensions/index.md#plugin_lifecycle).


<details>
<summary>MaterialsPlugin.cpp | Close</summary>

**MaterialsPlugin.cpp**


```cpp
#include "MaterialsPlugin.h"
#include "MaterialsView.h"
#include "MaterialsModel.h"
#include "QtMetaTypes.h"

#include <editor/UnigineActions.h>
#include <editor/UnigineUndo.h>
#include <editor/UnigineConstants.h>
#include <editor/UnigineWindowManager.h>
#include <editor/UnigineSelection.h>
#include <editor/UnigineSelector.h>

#include <QObject>
#include <QMenu>

#include <algorithm>
#include <iterator>

using ::UnigineEditor::Selection;
using ::UnigineEditor::SelectionAction;
using ::UnigineEditor::WindowManager;
using ::UnigineEditor::SelectorGUIDs;

namespace Materials
{

MaterialsPlugin::~MaterialsPlugin() = default;

bool MaterialsPlugin::init()
{
	model_ = new MaterialsModel(this);

	view_ = new MaterialsView(model_);
	view_->setWindowTitle("Plugin - Material List");
	view_->setObjectName("PluginMaterialsView");
	WindowManager::add(view_, WindowManager::ROOT_AREA_LEFT);
	connect(view_, &MaterialsView::selected, this, &MaterialsPlugin::setGlobalSelection);

	QMenu *menu = WindowManager::findMenu(::UnigineEditor::Constants::MM_WINDOWS);
	action_ = menu->addAction("Plugin - Material List", this, &MaterialsPlugin::showView);

	connect(Selection::instance(), &Selection::changed,
			this, &MaterialsPlugin::globalSelectionChanged);

	return true;
}

void MaterialsPlugin::shutdown()
{
	QMenu *menu = WindowManager::findMenu(::UnigineEditor::Constants::MM_WINDOWS);
	menu->removeAction(action_);
	action_ = nullptr;

	disconnect(
		Selection::instance(), &Selection::changed, this, &MaterialsPlugin::globalSelectionChanged);

	disconnect(view_);
	WindowManager::remove(view_);

	delete view_;
	view_ = nullptr;

	delete model_;
	model_ = nullptr;
}

void MaterialsPlugin::showView()
{
	WindowManager::show(view_);
}

void MaterialsPlugin::setGlobalSelection(const QModelIndexList &indexes)
{
	disconnect(Selection::instance(), &Selection::changed,
			this, &MaterialsPlugin::globalSelectionChanged);

	Unigine::Vector<Unigine::UGUID> guids;
	guids.reserve(indexes.size());
	std::transform(std::begin(indexes), std::end(indexes), std::back_inserter(guids),
			[](const QModelIndex &idx)
			{ return idx.data(MaterialsModel::GUID_ROLE).value<Unigine::UGUID>(); });
	SelectionAction::applySelection(SelectorGUIDs::createMaterialsSelector(guids));

	connect(Selection::instance(), &Selection::changed,
			this, &MaterialsPlugin::globalSelectionChanged);
}

void MaterialsPlugin::globalSelectionChanged()
{
	using namespace std;

	if (auto selector = Selection::getSelectorMaterials())
	{
		const Unigine::Vector<Unigine::UGUID> &guids = selector->guids();
		QModelIndexList indexes;
		indexes.reserve(guids.size());
		transform(begin(guids), end(guids), back_inserter(indexes),
				[this](const Unigine::UGUID &guid) { return model_->index(guid); });

		auto it = remove(begin(indexes), end(indexes), QModelIndex());
		indexes.erase(it, end(indexes));

		QSignalBlocker blocker(view_);
		view_->globalSelectionChanged(indexes);
	}
	else if (auto selector = Selection::getSelectorRuntimes())
	{
		// implementation
	}
	else
	{
		view_->clearSelection();
	}
}

} // namespace Materials

```

</details>


### Model Class


#### Header File


<details>
<summary>MaterialsModel.h | Close</summary>

**MaterialsModel.h**


```cpp
#pragma once

#include <QAbstractItemModel>

#include <UnigineGUID.h>

namespace Materials
{

class MaterialsModel final : public QAbstractItemModel
{
	class Item;
	Q_DISABLE_COPY(MaterialsModel)
public:
	enum Role
	{
		GUID_ROLE = Qt::UserRole + 1
	};

	explicit MaterialsModel(QObject *parent = nullptr);
	~MaterialsModel() override;

	QModelIndex index(int row, int column, const QModelIndex &parent = QModelIndex()) const override;
	QModelIndex index(const Unigine::UGUID &guid) const;
	QModelIndex parent(const QModelIndex &child) const override;
	int rowCount(const QModelIndex &parent = QModelIndex()) const override;
	int columnCount(const QModelIndex &parent = QModelIndex()) const override;
	QVariant data(const QModelIndex &index, int role = Qt::DisplayRole) const override;

protected:
	void fetchMore(const QModelIndex &parent) override;
	bool canFetchMore(const QModelIndex &parent) const override;

private:
	Item *const root_;
};

} // namespace Materials

```

</details>


#### Implementation File


<details>
<summary>MaterialsModel.cpp | Close</summary>

**MaterialsModel.cpp**


```cpp
#include "MaterialsModel.h"
#include "QtMetaTypes.h"
#include <UnigineMaterials.h>
#include <UnigineFileSystem.h>

#include <QDebug>

using Unigine::UGUID;

namespace Materials
{

////////////////////////////////////////////////////////////////////////////////
// MaterialsModel::Item.
////////////////////////////////////////////////////////////////////////////////
class MaterialsModel::Item
{
public:
	static Item *createRootItem(MaterialsModel *model);

	Item(Item *parent, MaterialsModel *model, const UGUID &guid);
	~Item();

	QModelIndex index() const;

	void append(Item *item);
	Item *child(int idx);
	Item *find(const UGUID &guid) const;
	int childCount() const;

	Item *parent();
	int row() const;
	QVariant data(int role) const;

	void fetchMore();
	bool canFetchMore() const;

private:
	Item *parent_ = nullptr;			// not owned
	MaterialsModel *model_ = nullptr;	// not owned
	QVector<Item *> children_;			// owned
	UGUID guid_;
};

MaterialsModel::Item *MaterialsModel::Item::createRootItem(MaterialsModel *model)
{
	Item *root = new Item(nullptr, model, UGUID());
	const int size = Unigine::Materials::getNumMaterials();
	for (int i = 0; i < size; ++i)
	{
		const Unigine::MaterialPtr mat = Unigine::Materials::getMaterial(i);
		if (mat->isHidden())
		{
			continue;
		}
		if (const Unigine::MaterialPtr &parent_mat = mat->getParent())
		{
			if (!parent_mat->isHidden())
			{
				continue;
			}
		}
		root->children_.push_back(new Item(root, model, mat->getGUID()));
	}
	return root;
}

MaterialsModel::Item::Item(Item *parent, MaterialsModel *model, const UGUID &guid)
	: parent_(parent), model_(model), guid_(guid)
{
}

MaterialsModel::Item::~Item()
{
	qDeleteAll(children_);
}

QModelIndex MaterialsModel::Item::index() const
{
	if (!parent_ || guid_.isEmpty())
	{
		return QModelIndex();
	}
	return model_->createIndex(row(), 0, const_cast<Item *>(this));
}

void MaterialsModel::Item::append(Item *item)
{
	const int size = children_.size();
	model_->beginInsertRows(index(), size, size);
	item->parent_ = this;
	children_.push_back(item);
	model_->endInsertRows();
}

auto MaterialsModel::Item::child(int idx) -> Item *
{
	return ((idx >= 0) && (idx < children_.size()))
		? children_[idx]
		: nullptr;
}

auto MaterialsModel::Item::find(const UGUID &guid) const -> Item *
{
	for (Item *child: children_)
	{
		if (child->guid_ == guid)
		{
			return child;
		}
		if (child->canFetchMore())
		{
			child->fetchMore();
		}
		if (Item *grandchild = child->find(guid))
		{
			return grandchild;
		}
	}
	return nullptr;
}

int MaterialsModel::Item::childCount() const
{
	if (!guid_.isValid())
	{
		return children_.size();
	}

	const Unigine::MaterialPtr mat = Unigine::Materials::findMaterialByGUID(guid_);
	if (!mat)
	{
		// TODO: handle processes of adding new materials and removing old ones

		return 0;
	}

	int count = mat->getNumChildren();
	for (int i = count - 1; i >= 0; --i)
	{
		if (mat->getChild(i)->isHidden())
		{
			--count;
		}
	}
	return count;
}

MaterialsModel::Item *MaterialsModel::Item::parent()
{
	return parent_;
}

int MaterialsModel::Item::row() const
{
	if (parent_)
	{
		return parent_->children_.indexOf(const_cast<Item *>(this));
	}
	return 0;
}

QVariant MaterialsModel::Item::data(int role) const
{
	if (Qt::DisplayRole == role)
	{
		const Unigine::MaterialPtr &mat = Unigine::Materials::findMaterialByGUID(guid_);
		if (!mat)
		{
			// TODO: handle processes of adding new materials and removing old ones

			const QString name =
				tr("Removed - %1").arg(QLatin1String(guid_.makeString().get()));
			return QVariant::fromValue(name);
		}

		const UGUID &file_mat_guid = Unigine::FileSystem::getGUID(mat->getPath());
		const UGUID &asset_guid = Unigine::FileSystemAssets::resolveAsset(file_mat_guid);
		const Unigine::String &virtual_path = Unigine::FileSystem::getVirtualPath(asset_guid);
		const Unigine::StringStack<> file_name = Unigine::String::filename(virtual_path);
		return QVariant::fromValue(QString(file_name.get()));
	}
	if (MaterialsModel::GUID_ROLE == role)
	{
		return QVariant::fromValue(guid_);
	}
	return QVariant();
}

void MaterialsModel::Item::fetchMore()
{
	const Unigine::MaterialPtr &mat = Unigine::Materials::findMaterialByGUID(guid_);
	if (!mat)
	{
		// TODO: handle processes of adding new materials and removing old ones

		return;
	}

	const int size = mat->getNumChildren();
	QVector<Item *> items;
	items.reserve(size);

	for (int i = 0; i < size; ++i)
	{
		const Unigine::MaterialPtr child_mat = mat->getChild(i);
		if (child_mat->isHidden())
		{
			continue;
		}
		items.push_back(new Item(this, model_, child_mat->getGUID()));
	}

	if (items.empty())
	{
		return;
	}

	const int cur_size = children_.size();
	model_->beginInsertRows(index(), cur_size, cur_size + items.size() - 1);
	std::copy(std::begin(items), std::end(items), std::back_inserter(children_));
	model_->endInsertRows();
}

bool MaterialsModel::Item::canFetchMore() const
{
	return children_.empty() && childCount();
}

////////////////////////////////////////////////////////////////////////////////
// MaterialsModel.
////////////////////////////////////////////////////////////////////////////////
MaterialsModel::MaterialsModel(QObject *parent)
	: QAbstractItemModel(parent)
	, root_(Item::createRootItem(this))
{
}

MaterialsModel::~MaterialsModel()
{
	delete root_;
}

QModelIndex MaterialsModel::index(int row, int column, const QModelIndex &parent) const
{
	if (column > 0)
	{
		return {};
	}

	Item *parent_item = nullptr;
	if (!parent.isValid())
	{
		parent_item = root_;
	}
	else
	{
		parent_item = static_cast<Item *>(parent.internalPointer());
	}

	Item *child_item = parent_item->child(row);
	return child_item
		? createIndex(row, column, child_item)
		: QModelIndex();
}

QModelIndex MaterialsModel::index(const UGUID &guid) const
{
	if (guid.isEmpty())
	{
		return QModelIndex();
	}
	Item *item = root_->find(guid);
	return item ? item->index() : QModelIndex();
}

QModelIndex MaterialsModel::parent(const QModelIndex &child) const
{
	if (!child.isValid())
	{
		return QModelIndex();
	}
	Item *child_item = static_cast<Item *>(child.internalPointer());
	Item *parent_item = child_item->parent();

	return (parent_item != root_)
		? createIndex(parent_item->row(), 0, parent_item)
		: QModelIndex();
}

int MaterialsModel::rowCount(const QModelIndex &parent) const
{
	if (parent.column() > 0)
	{
		return 0;
	}

	Item *parent_item = nullptr;
	if (!parent.isValid())
	{
		parent_item = root_;
	}
	else
	{
		parent_item = static_cast<Item *>(parent.internalPointer());
	}

	return parent_item->childCount();
}

int MaterialsModel::columnCount(const QModelIndex &parent) const
{
	return 1;
}

QVariant MaterialsModel::data(const QModelIndex &index, int role) const
{
	if (!index.isValid())
	{
		return QVariant();
	}

	Item *item = static_cast<Item *>(index.internalPointer());
	return item->data(role);
}

void MaterialsModel::fetchMore(const QModelIndex &parent)
{
	if (!parent.isValid())
	{
		return;
	}
	Item *item = static_cast<Item *>(parent.internalPointer());
	item->fetchMore();
}

bool MaterialsModel::canFetchMore(const QModelIndex &parent) const
{
	if (!parent.isValid())
	{
		return false;
	}
	Item *item = static_cast<Item *>(parent.internalPointer());
	return item->canFetchMore();
}

} // namespace Materials

```

</details>


### View Class


#### Header File


<details>
<summary>MaterialsView.h | Close</summary>

**MaterialsView.h**


```cpp
#pragma once

#include <QWidget>
#include <QModelIndex>

#include <UnigineGUID.h>

class QAbstractItemModel;
class QItemSelection;
class QTreeView;

namespace Materials
{

class MaterialsView : public QWidget
{
	Q_OBJECT
	Q_DISABLE_COPY(MaterialsView)
public:
	explicit MaterialsView(QAbstractItemModel *model, QWidget *parent = nullptr);
	~MaterialsView() override;

signals:
	void selected(const QModelIndexList &indexes);

public slots:
	void clearSelection();
	void globalSelectionChanged(const QModelIndexList &indexes);

private slots:
	void selectionChanged(const QItemSelection &selection);

private:
	QTreeView *view_ = nullptr;
};

} // namespace Materials

```

</details>


#### Implementation File


<details>
<summary>MaterialsView.cpp | Close</summary>

**MaterialsView.cpp**


```cpp
#include "MaterialsView.h"

#include <QAbstractItemModel>
#include <QVBoxLayout>
#include <QTreeView>

namespace Materials
{

MaterialsView::MaterialsView(QAbstractItemModel *model, QWidget *parent)
	: QWidget{parent}
{
	view_ = new QTreeView();
	view_->setAlternatingRowColors(true);
	view_->setSelectionMode(QAbstractItemView::ExtendedSelection);
	view_->setSelectionBehavior(QAbstractItemView::SelectRows);
	view_->setHeaderHidden(true);

	auto vl = new QVBoxLayout(this);
	vl->setContentsMargins(2, 2, 2, 2);
	vl->addWidget(view_);

	view_->setModel(model);

	connect(view_->selectionModel(), &QItemSelectionModel::selectionChanged
			, this, &MaterialsView::selectionChanged);
}

MaterialsView::~MaterialsView() = default;

void MaterialsView::clearSelection()
{
	view_->selectionModel()->clearSelection();
}

void MaterialsView::globalSelectionChanged(const QModelIndexList &indexes)
{
	if (indexes.empty())
	{
		clearSelection();
		return;
	}

	view_->setCurrentIndex(indexes.back());

	QItemSelection item_selection;
	for (const QModelIndex &index: indexes)
	{
		item_selection.append(QItemSelectionRange(index));
	}
	view_->selectionModel()->select(item_selection, QItemSelectionModel::ClearAndSelect);

	view_->scrollTo(indexes.back());
}

void MaterialsView::selectionChanged(const QItemSelection &selection)
{
	emit selected(view_->selectionModel()->selectedIndexes());
}

} // namespace Materials

```

</details>


### Auxiliary File


This file contains registration of additional metatypes to be used in our plugin. To make them known to Qt's meta-object system (to be able to put and get *Unigine::UGUID* to and out of the *[QVariant](https://doc.qt.io/qt-5/qvariant.html)*), we need *[Unigine::UGUID](../../api/library/filesystem/class.uguid_cpp.md)*.


> **Notice:** This file should be saved to the `source` folder with all other source files.


<details>
<summary>QtMetaTypes.h | Close</summary>

**QtMetaTypes.h**


```cpp
#pragma once

// including UnigineGUID.h containing definition of the metatype we're going to declare
#include <UnigineGUID.h>
// including QMetaType to be able to declare metatypes
#include <QMetaType>

// registering the Unigine::UGUID type to make it known to Qt's meta-object system
Q_DECLARE_METATYPE(Unigine::UGUID)

```

</details>


## Building the Plugin


### Using MS Visual Studio


In case you're using *MS Visual Studio*, there is a `.vcxproj` file in your plugin folder just select the *Release* configuration and choose *Build Solution* in the main menu. The project is pre-configured to launch with the UnigineEditor so you can run and test it right from your IDE (e.g. simply hit the default *Ctrl + F5* hotkey in *Visual Studio*).


> **Notice:** *Release* version of the Editor requires *Release* binaries of plugins and does not load *Debug* ones!


### Using CMake


All files required to build our plugin using CMake (`CMakeList.txt` and `Materials.json` describing our *Materials* plugin and its dependencies) are automatically added to the corressponding folder of your plugin inside your UNIGINE project's `source` folder. So, launch CMake to build the plugin.


## Running the Plugin


As the plugin is built, all resulting files are automatically copied to the `%project_name%/bin/plugins/Unigine/` folder, so that [UnigineEditor Plugin System](../../editor2/extensions/index.md#plugin_system) could load it automatically.


And finally we launch UnigineEditor to check our plugin. If everything was done properly, you will see the **MaterialsPlugin** plugin in *Editor Plugin Manager* (*Windows -> Editor Plugin Manager*).


![Plugins List](pluginslistview.png)


> **Notice:** You can **unload** and **load** your plugin again when necessary via the corresponding button in the **HotReload** column.
