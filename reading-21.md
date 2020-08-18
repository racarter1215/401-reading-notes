# Components

### They are similar to partial views and don't use model binding, and only depend on the data provided when calling into it.

##### consists of two parts: the class and the result it returns

##### A view component class can be created by any of the following:

##### Deriving from ViewComponent
##### Decorating a class with the [ViewComponent] attribute, or deriving from a class with the [ViewComponent] attribute
##### Creating a class where the name ends with the suffix ViewComponent
##### View components must be public, non-nested, and non-abstract classes. The view component name is the class name with the "ViewComponent" suffix removed. 
#####It can also be explicitly specified using the ViewComponentAttribute.Name property.

##### View component defines its logic in an InvokeAsync method
##### It returns a Task<IViewComponentResult> or in a synchronous Invoke method that returns an IViewComponentResult.

##### runtime searches look for these paths:
/Views/{Controller Name}/Components/{View Component Name}/{View Name}
/Views/Shared/Components/{View Component Name}/{View Name}
/Pages/Shared/Components/{View Component Name}/{View Name}

##### Example of customizing view search:
services.AddMvc()
    .AddRazorOptions(options =>
    {
        options.ViewLocationFormats.Add("/{0}.cshtml");
    })
    .SetCompatibilityVersion(CompatibilityVersion.Version_2_2);

##### Example of adding view component class:
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using ViewComponentSample.Models;

namespace ViewComponentSample.ViewComponents
{
    public class PriorityListViewComponent : ViewComponent
    {
        private readonly ToDoContext db;

        public PriorityListViewComponent(ToDoContext context)
        {
            db = context;
        }

        public async Task<IViewComponentResult> InvokeAsync(
        int maxPriority, bool isDone)
        {
            var items = await GetItemsAsync(maxPriority, isDone);
            return View(items);
        }
        private Task<List<TodoItem>> GetItemsAsync(int maxPriority, bool isDone)
        {
            return db.ToDo.Where(x => x.IsDone == isDone &&
                                 x.Priority <= maxPriority).ToListAsync();
        }
    }
}

##### 
