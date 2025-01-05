# gleam basic examples

## Hello. It's basic gleam code examples that you can use or look to understand how you can think through gleam language


### String interpolation

```gleam
import gleam/string.{drop_end, drop_start, ends_with, length, starts_with}
pub fn replace(
  in format_string: String,
  replace label: String,
  with data: a,
) -> String {
  let to_replace = "{" <> label <> "}"
  let inspected_string = string.inspect(data)

  let str = case
    //cut of " from stard and end string 
    ends_with(inspected_string, "\"")
    && starts_with(inspected_string, "\"")
    //if there's just two " it will not cut "
    //you can delete it if you want
    && length(inspected_string) > 2
  {
    False -> inspected_string
    True -> inspected_string |> drop_start(1) |> drop_end(1)
  }

  string.replace(in: format_string, each: to_replace, with: str)
}

pub fn exmaple() {
  let path =
    "{db}/_design/{design}/_view/{view}"
    |> replace("db", "some_db_name")
    |> replace("design", "design_name")
    |> replace("view", "view_name")
  path
}

```
