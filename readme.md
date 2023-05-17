# How to add Swaagger

First ,install swagger to project
***

1.Install Swagger

```bash
go get github.com/swaggo/swag/cmd/swag 
```

2.Install swagger files

```bash
go get github.com/swaggo/files 
```

3.Install gin-swagger

```bash
go get github.com/swaggo/gin-swagger  
```

Secord ,add swagger at router
***
```golang
router.GET("/docs/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))
```

Third ,add Description
***

```golang
// CreateTags		godoc
// @Summary			Create tags
// @Description		Save tags data in Db
// @Param			tags body request.CreateTagsRequest true "Create tags"
// @Produce 		application/json
// @Tags 			tags
// @Success 		200 {object} response.Response{}
// @Router 			/tags [post]
func (controller *TagsController) Create(ctx *gin.Context) {
	createTagsRequest := request.CreateTagsRequest{}
	err := ctx.ShouldBindJSON(&createTagsRequest)
	helper.ErrorPanic(err)

	controller.tagsService.Create(createTagsRequest)
	webResponse := response.Response{
		Code:   http.StatusOK,
		Status: "Ok",
		Data:   nil,
	}
	ctx.Header("Content-Type", "application/json")
	ctx.JSON(http.StatusOK, webResponse)
}
```

Last ,init swagger into project

```bash
swag init   
```
