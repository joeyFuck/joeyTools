```java
@GetMapping("/get")
public String get() {
    return "get";
}

@PostMapping("/post")
public String post(@RequestParam(value = "param") String param) {
    return param;
}

@DeleteMapping("/delete/{id}")
public String delete(@PathVariable(value = "id") Integer id) {
    return id.toString();
}

@PutMapping("/put")
public String put() {
    return "put";
}

@PatchMapping("/patch")
public String patch() {
    return "patch";
}

```


```java
@PostMapping("/field/form/save")
public Result saveFieldForm(@RequestBody VLayoutFieldFormEntity params) {
  VLayoutFieldFormEntity entity = vLayoutFieldFormService.saveOrUpdateField(params);
  return ResultUtil.success(entity);
}

@PostMapping("/type/delete")
public Result deleteFieldWidthType(@RequestBody Map<String, String> params){
    vLayoutFieldService.deleteFieldListWithType(params);
    return ResultUtil.success();
}

@RequestMapping(value = {"/field/list/{id}","/field/list/{id}/filter/{content}"})
public Result getFieldList(@PathVariable(name = "id") String id,@PathVariable(name = "content",required = false) String content) {
    List list = vLayoutFieldService.queryFieldList(id,content);
    return ResultUtil.success(list);
}
```
