# How-to-Select-a-Row-Using-Right-Click-in-a-Flutter-DataTable

In this article, we will show you how to select a row using a right-click in a [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the required configurations.  To handle `right-click` actions, use the [onCellSecondaryTap](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/onCellSecondaryTap.html) callback, which is triggered when a user performs a secondary mouse click on a cell.

Within the callback, verify that the application is running on a supported platform and ensure that the clicked row is not the header row. Then, use the [selectedIndex](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridController/selectedIndex.html) property of the [DataGridController](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridController-class.html) to select the corresponding record.

Because the `DataGrid` row index includes the header row, subtract 1 from the tapped row index before assigning it to the controller. This adjustment ensures that the correct data row is selected when the user right-clicks on a cell.

```dart

  // DataGridController to manage the selection operations of the DataGrid.
  late DataGridController _dataGridController;
  
  @override
  void initState() {
    super.initState();
    _dataGridController =
        DataGridController(); // Initialize the DataGridController.
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Syncfusion Flutter DataGrid')),
      body: SfDataGrid(
        source: employeeDataSource,
        controller:
            _dataGridController, // Assign the DataGridController to the DataGrid.
        selectionMode:
            SelectionMode.single, // Set the selection mode as required.
        columnWidthMode: ColumnWidthMode.fill,
        onCellSecondaryTap: (details) {
          // Handle the right-click event on the DataGrid cells.
          // Add Platform limitation as required for bussinees logic.
          if (!Platform.isWindows) {
            return;
          }

          // Add the row index check to avoid the selection of header row.
          if (details.rowColumnIndex.rowIndex <= 0) {
            return;
          }

          // Set the selected index of the DataGridController to the row index of the tapped cell.
          final int rowIndex = details.rowColumnIndex.rowIndex - 1;

          // Set the selected index of the DataGridController to the row index of the tapped cell.
          _dataGridController.selectedIndex = rowIndex;
        },
        columns: <GridColumn>[
          GridColumn(
            columnName: 'id',
            label: Container(
              padding: EdgeInsets.all(16.0),
              alignment: Alignment.center,
              child: Text('ID'),
            ),
          ),
          GridColumn(
            columnName: 'name',
            label: Container(
              padding: EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: Text('Name'),
            ),
          ),
          GridColumn(
            columnName: 'designation',
            label: Container(
              padding: EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: Text('Designation', overflow: TextOverflow.ellipsis),
            ),
          ),
          GridColumn(
            columnName: 'salary',
            label: Container(
              padding: EdgeInsets.all(8.0),
              alignment: Alignment.center,
              child: Text('Salary'),
            ),
          ),
        ],
      ),
    );
  }

```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-Select-a-Row-Using-Right-Click-in-a-Flutter-DataTable).