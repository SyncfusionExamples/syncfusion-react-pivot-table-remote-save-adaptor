<div align="center">
  <h1>Syncfusion® React Pivot Table – Remote Save Adaptor Quick Start</h1>

  <p>
    A ready-to-run quick start that connects the <strong>Syncfusion® React Pivot Table</strong> to an <strong>ASP.NET Core Web API</strong> backend using the <strong>RemoteSaveAdaptor</strong> — combining instant client-side operations (filter, sort, page, search, group) with server-side CRUD persistence.
  </p>

  <p>
    <a href="https://react.dev/"><img src="https://img.shields.io/badge/React-18%2B-61DAFB?style=for-the-badge&logo=react&logoColor=white" alt="React"></a>
    <a href="https://dotnet.microsoft.com/apps/aspnet"><img src="https://img.shields.io/badge/.NET-8.0%2B-512BD4?style=for-the-badge&logo=dotnet&logoColor=white" alt=".NET"></a>
    <a href="https://www.syncfusion.com/react-components/react-pivot-table"><img src="https://img.shields.io/badge/Syncfusion-EJ2-FF9C00?style=for-the-badge&logo=syncfusion&logoColor=white" alt="Syncfusion"></a>
    <a href="https://github.com/SyncfusionExamples/remote-save-adaptor-with-pivot-table/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"></a>
  </p>
</div>

---

## 📑 Table of Contents

- [🚀 Quick Overview](#-quick-overview)
- [✨ Key Features](#-key-features)
- [🧠 What is RemoteSaveAdaptor?](#-what-is-remotesaveadaptor)
- [🛠️ Prerequisites](#-prerequisites)
- [📂 Project Structure](#-project-structure)
- [⚙️ Installation & Setup](#-installation--setup)
  - [1. Clone the Repository](#1-clone-the-repository)
  - [2. Backend – ASP.NET Core Web API](#2-backend--aspnet-core-web-api)
  - [3. Frontend – React Pivot Table](#3-frontend--react-pivot-table)
- [▶️ Running the Application](#-running-the-application)
- [🧪 Testing CRUD Operations](#-testing-crud-operations)
- [📊 Data Flow & Adaptor Behavior](#-data-flow--adaptor-behavior)
- [🔧 Troubleshooting](#-troubleshooting)
- [📖 API Reference](#-api-reference)
- [🤝 Contributing](#-contributing)
- [📜 License & Support](#-license--support)
- [📚 Related Resources](#-related-resources)

---

## 🚀 Quick Overview

This project demonstrates how to bind the **Syncfusion® React Pivot Table** to a remote **ASP.NET Core Web API** backend using the [`RemoteSaveAdaptor`](https://ej2.syncfusion.com/react/documentation/data/adaptors/remote-save-adaptor) of the [`DataManager`](https://ej2.syncfusion.com/react/documentation/data/getting-started).

The `RemoteSaveAdaptor` provides a **hybrid data-binding strategy**:

- 🔹 **One initial load** — all records are fetched from the server once.
- 🔹 **Client-side operations** — filtering, sorting, paging, searching, and grouping happen instantly in the browser.
- 🔹 **Server-side CRUD** — only **insert, update, and delete** operations are sent back to the server.

| Component          | Technology                         | Purpose                                              |
| ------------------ | ---------------------------------- | ---------------------------------------------------- |
| 🎨 Frontend        | React 18+ + Syncfusion® EJ2        | Render the interactive Pivot Table UI                |
| ⚙️ Backend         | ASP.NET Core (.NET 8.0+)           | Serve all records on load + handle CRUD requests    |
| 🔌 Adaptor         | `RemoteSaveAdaptor`                | Hybrid bridge — client-side reads, server-side writes |
| 📊 Sample Data     | In-memory `OrdersDetails` list     | Seed records for the Pivot Table                     |

> 💡 Use `RemoteSaveAdaptor` when you want the **snappy feel of client-side data** but still need **persistent, server-backed writes**.

---

## ✨ Key Features

- 🔀 **Hybrid Data Binding** — read operations on the client, write operations on the server.
- ⚡ **Instant UX** — filter, sort, page, search, and group without round-trips to the server.
- 🗄️ **Server-side CRUD** — `Insert`, `Update`, and `Remove` actions persisted via dedicated API endpoints.
- 🧾 **Drill-Through Editing** — double-click a pivot cell to add, edit, or delete underlying records.
- 🔑 **Primary Key Configuration** — `OrderID` is marked as the primary key in the drill-through grid.
- 🌐 **CORS-Enabled** — preconfigured to allow cross-origin requests from the React dev server.
- 🛡️ **Property Casing Preservation** — uses `DefaultContractResolver` so PascalCase fields like `OrderID`, `CustomerID` are preserved.
- 📦 **Ready-to-Run** — clone, build, and start both projects — no database setup required (in-memory sample data).

---

## 🧠 What is RemoteSaveAdaptor?

`RemoteSaveAdaptor` is a specialized adaptor that splits data operations into **two categories** based on whether they modify data or simply read it.

**Server-side operations (requires server requests):**

- Create (Insert)
- Update (Edit)
- Delete (Remove)

**Data flow:**

1. **Initial load** — Fetches all data from the server once.
2. **User interactions** — Filtering, sorting, paging, searching, and grouping happen instantly in the browser.
3. **Data changes** — Only CRUD operations (add, edit, delete) send requests to the server.
4. **Result** — Fast UI with secure data persistence.

### When to use RemoteSaveAdaptor?

✅ **Good fit**

- Medium-sized datasets (1K–50K records that fit in browser memory)
- Need instant filtering, sorting, and paging without server delay
- Many read operations, few write operations
- Want to reduce server load for common operations
- Network latency is a concern
- Users frequently switch between filters, sorts, and pages

❌ **Not a good fit** — consider `UrlAdaptor` or `ODataV4Adaptor` instead

- Very large datasets (100K+ records)
- Data changes frequently on the server (real-time updates)
- Memory-constrained client devices
- Complex server-side business logic for filtering
- Limited bandwidth for initial data load

---

## 🛠️ Prerequisites

Make sure the following software and packages are installed before running the project.

| Software / Package                              | Version       | Purpose                                                  |
| ----------------------------------------------- | ------------- | -------------------------------------------------------- |
| 🟢 Node.js                                      | 18.x or later | Runtime for the React development server                 |
| ⚛️ React                                        | 18.x or later | Build the Pivot Table client                             |
| 🟣 .NET SDK                                     | 8.0 or later  | Build and run the ASP.NET Core Web API                   |
| 🧑‍💻 Visual Studio / VS Code                    | Latest        | Configure and run the backend API                        |
| 📦 `@syncfusion/ej2-react-pivotview`            | 33.1.45+      | React Pivot Table component                              |
| 📦 `@syncfusion/ej2-data`                       | 33.1.45+      | `DataManager` and `RemoteSaveAdaptor`                    |
| 📦 `Microsoft.AspNetCore.Mvc.NewtonsoftJson`    | 8.0+          | Preserve original PascalCase property names during JSON  |

---

## 📂 Project Structure

```
remote-save-adaptor-with-pivot-table/
├── 📁 Client/                              # React frontend (Pivot Table)
│   ├── 📁 public/
│   │   ├── index.html
│   │   ├── manifest.json
│   │   └── robots.txt
│   ├── 📁 src/
│   │   ├── App.css                         # Component styles
│   │   ├── App.js                          # Pivot Table with RemoteSaveAdaptor configuration
│   │   ├── App.test.js
│   │   ├── datasource.js                   # Local pivot data (alternate sample)
│   │   ├── index.css
│   │   ├── index.js                        # React entry point
│   │   ├── reportWebVitals.js
│   │   └── setupTests.js
│   └── package.json                        # React dependencies & scripts
│
├── 📁 RemoteSaveAdaptor/                   # ASP.NET Core Web API backend
│   ├── 📁 Controllers/
│   │   └── OrdersController.cs              # Endpoints: GET, POST, Insert, Update, Remove
│   ├── 📁 Models/
│   │   └── OrdersDetails.cs                # Order data model + sample data
│   ├── 📁 Properties/
│   │   └── launchSettings.json
│   ├── appsettings.Development.json
│   ├── appsettings.json
│   ├── Program.cs                          # CORS + Newtonsoft.Json configuration
│   ├── RemoteSaveAdaptor.csproj            # Project file
│   └── RemoteSaveAdaptor.http              # Endpoint testing file
│
├── 📄 README.md                            # You are here
```

---

## ⚙️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/SyncfusionExamples/remote-save-adaptor-with-pivot-table.git
cd remote-save-adaptor-with-pivot-table
```

### 2. Backend – ASP.NET Core Web API

The backend project lives in the `RemoteSaveAdaptor/` folder.

#### 2.1 Restore dependencies

```bash
cd RemoteSaveAdaptor
dotnet restore
```

#### 2.2 Verify the required NuGet package

Ensure `Microsoft.AspNetCore.Mvc.NewtonsoftJson` is referenced in `RemoteSaveAdaptor.csproj`. It is required so the API serializes properties using their original PascalCase names (`OrderID`, `CustomerID`, etc.) instead of the default camelCase.

```bash
dotnet add package Microsoft.AspNetCore.Mvc.NewtonsoftJson
```

#### 2.3 Inspect the configuration

`Program.cs` already configures:

- ✅ **NewtonsoftJson** with `DefaultContractResolver` to preserve property casing.
- ✅ **CORS** with `AllowAnyOrigin` for development (restrict this in production).
- ✅ **Controllers** mapped via `MapControllers()`.

```csharp
// filepath: RemoteSaveAdaptor/Program.cs
using Newtonsoft.Json.Serialization;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddMvc().AddNewtonsoftJson(options =>
{
    options.SerializerSettings.ContractResolver = new DefaultContractResolver();
});

builder.Services.AddCors(options =>
{
    options.AddDefaultPolicy(policy =>
    {
        policy.AllowAnyOrigin()
              .AllowAnyMethod()
              .AllowAnyHeader();
    });
});

builder.Services.AddControllers();
builder.Services.AddOpenApi();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.MapOpenApi();
}

app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
app.UseCors();

app.Run();
```

> 🔒 **Production CORS:** Replace `AllowAnyOrigin()` with `policy.WithOrigins("https://yourdomain.com")`.

### 3. Frontend – React Pivot Table

The React client lives in the `Client/` folder.

#### 3.1 Install npm dependencies

```bash
cd ../Client
npm install
```

#### 3.2 Verify the API URL

Open `src/App.js` and ensure the `serviceUrl` points to your backend port. The default in this repo is `5211` (as defined in `Properties/launchSettings.json`).

```jsx
// filepath: Client/src/App.js
import React, { useState, useEffect } from 'react';
import { PivotViewComponent } from '@syncfusion/ej2-react-pivotview';
import { DataManager, RemoteSaveAdaptor } from '@syncfusion/ej2-data';
import './App.css';

function App() {
    const serviceUrl = "http://localhost:5211/api/Orders"; // 👈 Update if your backend uses a different port

    const [data, setData] = useState(null);

    useEffect(() => {
        fetch(serviceUrl)
            .then((response) => response.json())
            .then((result) => {
                // Build the DataManager with the RemoteSaveAdaptor.
                // The full JSON payload is passed in via `json`, so the client
                // can perform filter/sort/page/group locally without further server calls.
                setData(new DataManager({
                    json: result,
                    adaptor: new RemoteSaveAdaptor(),
                    updateUrl: `${serviceUrl}/Update`,
                    insertUrl: `${serviceUrl}/Insert`,
                    removeUrl: `${serviceUrl}/Remove`,
                }));
            })
            .catch((error) => console.error("Error fetching data:", error));
    }, []);

    const editSettings = {
        allowEditing: true,
        allowAdding: true,
        allowDeleting: true,
        mode: 'Normal'
    };

    const dataSourceSettings = {
        dataSource: data,
        expandAll: false,
        rows: [{ name: 'CustomerID' }],
        columns: [{ name: 'OrderID' }],
        values: [{ name: 'Freight' }],
        formatSettings: [{ name: 'Freight', format: 'N0' }],
    };

    let pivotObj;

    // Configure beginDrillThrough to mark the primary key and adjust edit types.
    function beginDrillThrough(args) {
        for (var i = 0; i < args.gridObj.columns.length; i++) {
            if (args.gridObj.columns[i].field === "OrderID") {
                args.gridObj.columns[i].isPrimaryKey = true;
            } else {
                args.gridObj.columns[i].visible = true;
                if (args.gridObj.columns[i].field === 'OrderDate' || args.gridObj.columns[i].field === 'ShippedDate') {
                    args.gridObj.columns[i].editType = 'datetimepickeredit';
                }
            }
        }
    }

    return (
        <div className='control-section' style={{ margin: 100 }}>
            <PivotViewComponent
                ref={d => pivotObj = d}
                id='PivotView'
                height={350}
                width={700}
                editSettings={editSettings}
                beginDrillThrough={beginDrillThrough}
                dataSourceSettings={dataSourceSettings}>
            </PivotViewComponent>
        </div>
    );
}

export default App;
```

> 🔑 **Key points**
> - `json: result` — feeds the entire payload to the client immediately.
> - `RemoteSaveAdaptor` — splits operations between client (reads) and server (writes).
> - `insertUrl`, `updateUrl`, `removeUrl` — point the adaptor at the dedicated CRUD endpoints.

---

## ▶️ Running the Application

You need **two terminals** — one for the backend API and one for the React client.

### ▶️ Start the Backend (Terminal 1)

```bash
cd RemoteSaveAdaptor
dotnet run
```

The API will start on `http://localhost:5211` by default (per `Properties/launchSettings.json`).

**Verify it works:**

- 🌐 Open `http://localhost:5211/api/Orders` in your browser.
- ✅ You should see a JSON array of all seed order records (returned by the `GetOrderData` action).

> 📝 If the terminal shows a different port, update the `serviceUrl` constant in `Client/src/App.js` to match.

### ▶️ Start the Frontend (Terminal 2)

```bash
cd Client
npm start
```

The React app will open at `http://localhost:3000` by default. 🎉

You should see the Pivot Table populated with aggregated **Freight** values, grouped by **CustomerID** (rows) and **OrderID** (columns).

### ✅ Verify in the Browser

1. Open the browser's **Developer Tools** (F12) → **Network** tab.
2. Reload the page.
3. You should see **one** initial `GET http://localhost:5211/api/Orders` request that returns the full dataset.
4. Try filtering, sorting, or paging — **no new network requests** should appear (those happen client-side).
5. Open the drill-through grid and perform a CRUD operation — a new request will fire to `/Insert`, `/Update`, or `/Remove`.

---

## 🧪 Testing CRUD Operations

The Pivot Table supports full CRUD through its built-in **drill-through editing** grid.

| Step | Action                                                                                                  | Expected Network Request                                |
| ---- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| 1️⃣  | **Double-click** any pivot cell to open the drill-through grid showing the underlying source records.   | Initial `GET` to `/api/Orders`                           |
| ➕ 2️⃣ | Click **Add**, fill in the new row fields, then click **Update**.                                       | `POST http://localhost:5211/api/Orders/Insert`           |
| ✏️ 3️⃣ | Click **Edit** on an existing row, change a field, then click **Update**.                                | `POST http://localhost:5211/api/Orders/Update`           |
| 🗑️ 4️⃣ | Click **Delete** on a row to remove it.                                                                  | `POST http://localhost:5211/api/Orders/Remove`           |
| 🔁 5️⃣ | The Pivot Table automatically refreshes to display the updated aggregated data.                          | No additional request — refresh is client-side          |

> 🔑 The `OrderID` column is automatically marked as the primary key inside the `beginDrillThrough` event, so update and delete operations know which record to target.

---

## 📊 Data Flow & Adaptor Behavior

Understanding what travels over the wire and what stays in the browser is the key benefit of `RemoteSaveAdaptor`.

### Request map

| User action              | Where it runs | Server request? |
| ------------------------ | ------------- | --------------- |
| Initial page load        | Server        | ✅ `GET /api/Orders` |
| Apply a filter           | Browser       | ❌ |
| Sort a column            | Browser       | ❌ |
| Change page              | Browser       | ❌ |
| Search                   | Browser       | ❌ |
| Group / expand / collapse| Browser       | ❌ |
| **Insert** a record      | **Server**    | ✅ `POST /api/Orders/Insert` |
| **Update** a record      | **Server**    | ✅ `POST /api/Orders/Update` |
| **Delete** a record      | **Server**    | ✅ `POST /api/Orders/Remove` |

### Why a single initial load?

`RemoteSaveAdaptor` is built for datasets small enough to live in browser memory. Once that snapshot is loaded, every read interaction (filter, sort, page, search, group) is a pure in-memory operation, so the UI feels instant. The trade-off is that the **entire** dataset is fetched up front.

### CRUD payload shape

When the user inserts, updates, or removes a record, the adaptor POSTs a `CRUDModel<T>` to the relevant endpoint:

```csharp
public class CRUDModel<T> where T : class
{
    public string? action { get; set; }       // "insert" | "update" | "remove"
    public string? keyColumn { get; set; }    // e.g. "OrderID"
    public object? key { get; set; }          // value of the primary key
    public T? value { get; set; }             // the affected record
    public List<T>? added { get; set; }
    public List<T>? changed { get; set; }
    public List<T>? deleted { get; set; }
    public IDictionary<string, object>? @params { get; set; }
}
```

---

## 🔧 Troubleshooting

| ❓ Issue                                | 🔍 Symptom                                                                                                       | ✅ Resolution                                                                                                                |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 🚫 Empty Pivot Table                    | Pivot loads with no errors but no rows or values appear.                                                          | Ensure `serviceUrl` matches the backend port and that the initial `GET` returns a JSON array.                                 |
| 404 Not Found                           | Network tab shows a 404 response when the Pivot Table loads.                                                     | Confirm the backend is running and the route is `[Route("api/[controller]")]`. The controller is `Pivot`, so the URL is `/api/Orders`. |
| 💥 500 Internal Server Error            | The Pivot Table fails and the browser shows a server error.                                                      | Check the terminal/Visual Studio output for stack traces. Common causes: null reference or serialization issues.             |
| 🌐 CORS Blocked                         | Console shows `Access to XMLHttpRequest ... has been blocked by CORS policy`.                                    | Verify CORS is configured in `Program.cs` and that `app.UseCors()` is called **before** `app.MapControllers()`.               |
| 💾 CRUD operations not saving           | The edit dialog closes but changes are not reflected in the data.                                                | Confirm the primary key is set in `beginDrillThrough` and that `insertUrl`/`updateUrl`/`removeUrl` point to the right routes. |
| 🔤 Property casing mismatch             | Pivot appears empty or shows "field not found" even though the API returns data.                                 | Ensure `DefaultContractResolver` is registered in `Program.cs` so PascalCase fields like `OrderID` are preserved.             |
| 🐢 Initial load is slow                 | The first request takes a long time to return.                                                                  | You're sending the entire dataset at once. Consider shrinking it, or switch to `UrlAdaptor` for very large datasets.          |
| 🔒 SSL/TLS certificate error            | Console shows `net::ERR_CERT_AUTHORITY_INVALID` or browser warns about an untrusted certificate.                 | Run `dotnet dev-certs https --clean` then `dotnet dev-certs https --trust` (Windows/macOS). On Linux, use HTTP for local testing. |
| 💻 High memory usage in browser         | Browser tab consumes a lot of RAM after the page loads.                                                          | This is expected — `RemoteSaveAdaptor` holds the full dataset in memory. For 100K+ records, switch to `UrlAdaptor` or `ODataV4Adaptor`. |

---

## 📖 API Reference

The backend exposes the following endpoints through `OrdersController`:

| Method   | Route                       | Purpose                                                            | Request Body                  | Response                  |
| -------- | --------------------------- | ------------------------------------------------------------------ | ----------------------------- | ------------------------- |
| `GET`    | `/api/Orders`                | Retrieve all order records (used by the initial client load)       | —                             | JSON array of orders      |
| `POST`   | `/api/Orders`                | Return all records with count (`{ result, count }`)                | —                             | `{ result, count }`       |
| `POST`   | `/api/Orders/Insert`         | Insert a new order                                                 | `CRUDModel<OrdersDetails>`    | The newly inserted record |
| `POST`   | `/api/Orders/Update`         | Update an existing order (matched by `OrderID`)                    | `CRUDModel<OrdersDetails>`    | The updated record        |
| `POST`   | `/api/Orders/Remove`         | Remove an order by primary key                                     | `CRUDModel<OrdersDetails>`    | The deleted record        |

The `OrdersDetails` model exposes the following fields (additional fields are commented out in the model and can be re-enabled as needed):

| Field         | Type        | Description                                |
| ------------- | ----------- | ------------------------------------------ |
| `OrderID`     | `int?`      | Unique order identifier (primary key)      |
| `CustomerID`  | `string`    | Identifier of the customer                 |
| `EmployeeID`  | `int?`      | Identifier of the handling employee        |
| `Freight`     | `double?`   | Shipping cost                              |

> 📝 **Note:** The model in this sample is intentionally minimal (`OrderID`, `CustomerID`, `EmployeeID`, `Freight`). The other common fields (`ShipCity`, `Verified`, `OrderDate`, `ShipName`, `ShipCountry`, `ShippedDate`, `ShipAddress`) are present as commented-out members so you can enable them as your scenario grows.

---

## 🤝 Contributing

Contributions are welcome and appreciated! 💖

1. 🍴 **Fork** the repository.
2. 🌿 **Create** a feature branch: `git checkout -b feature/my-awesome-change`
3. 💾 **Commit** your changes: `git commit -m "Add my awesome change"`
4. 📤 **Push** to your branch: `git push origin feature/my-awesome-change`
5. 🔁 **Open** a Pull Request describing the change and its motivation.

### 📋 Contribution Guidelines

- Follow the existing code style in both the React and ASP.NET Core projects.
- Keep changes focused — one feature or fix per pull request.
- Update or add documentation (`README.md`, `remote-save-adaptor.md`) when behavior changes.
- Test your changes locally against both the backend and frontend before submitting.

---

## 📜 License & Support

### 📄 License

This project is released under the **MIT License**. You are free to use, modify, and distribute the code in personal and commercial projects. See the `LICENSE` file for full text.

### 🛟 Support

- 📘 **Documentation:** [Syncfusion® React Pivot Table Docs](https://ej2.syncfusion.com/react/documentation/pivotview/getting-started)
- 💬 **Community forum:** [Syncfusion® Community](https://www.syncfusion.com/forums)
- 🐛 **Bug reports & feature requests:** [GitHub Issues](https://github.com/SyncfusionExamples/remote-save-adaptor-with-pivot-table/issues)
- 📧 **Direct support:** [Syncfusion® Support Portal](https://www.syncfusion.com/support) (for licensed users)
- 📖 **Remote Save Adaptor Guide:** [RemoteSaveAdaptor Documentation](https://ej2.syncfusion.com/react/documentation/data/adaptors/remote-save-adaptor)

> ⭐ If this project helped you, please consider giving it a **star** on GitHub — it helps others discover it!

---

## 📚 Related Resources

- 🔗 [WebApiAdaptor with Pivot Table](https://github.com/SyncfusionExamples/webapi-adaptor-with-pivot-table) — Companion sample using `WebApiAdaptor` for full server-side OData queries.
- 🔗 [UrlAdaptor with Pivot Table](https://github.com/SyncfusionExamples/url-adaptor-with-pivot-table) — Companion sample using `UrlAdaptor` for full server-side control.
- 📘 [PivotTable Data Binding](https://ej2.syncfusion.com/react/documentation/pivotview/data-binding)
- 📘 [DataManager Getting Started](https://ej2.syncfusion.com/react/documentation/data/getting-started)
- 📘 [RemoteSaveAdaptor Reference](https://ej2.syncfusion.com/react/documentation/data/adaptors/remote-save-adaptor)
- 📘 [PivotTable Editing](https://ej2.syncfusion.com/react/documentation/pivotview/editing)
- 📘 [PivotTable Drill-Through](https://ej2.syncfusion.com/react/documentation/pivotview/drill-through)

---

<div align="center">
  <sub>Built with ❤️ using <a href="https://react.dev/">React</a> and <a href="https://dotnet.microsoft.com/">.NET</a> by the <a href="https://www.syncfusion.com/">Syncfusion®</a> team.</sub>
</div>
