Automigrate 

逻辑是判断表格是否存在， column是否存在，而不关注column的类型。所以期望去更改column类型是不可取的。当然这么做也是非常有道理的。因为类型的转换嘛，一定需要人去指定规则的。毕竟两种类型能直接互相转换的概率是非常小的 

 
```golang
type CrowdsourcingSegmentTask struct { 
    Model 
    Workflow 
    // 状态 
    Status int `json:"status" gorm:"index"` 
    // 属于的任务令 
    WorkorderID uint `json:"workorder_id"` 
    // 类型 
    Type CrowdsourcingSegmentTaskType `json:"type"` 
    // 骨架编号 
    SkeletonCode pq.StringArray `json:"skeleton_code" gorm:"type:text[];column:skeleton_codes"` 
    // 形状 
    Geom string `json:"geom"` 
    // 扩展形状 
    ExtendedGeom string `json:"extended_geom"` 
    // 流程实例UUID 
    WorkflowUUID string `json:"workflow_uuid"` 
    // 参数 
    Params []*CrowdsourcingSegmentTaskParam `json:"params"` 
    // 依赖的包任务 
    PackageTasks []*CrowdsourcingSplitedPackageTask `json:"-" gorm:"many2many:crowdsourcing_segment_task_splited_package_tasks;"` 
    // 归属的任务令 
    Workorder *Workorder `json:"workorder"` 
    // 包括此骨架的段任务 
    Skeleton []*Skeleton `json:"-" gorm:"many2many:segment_task_skeletons;"` 
} 
```

注意观察，　SkeletonCode字段中。判断column是否存在的依据首先是看column的取值，如果没有column,则会自动根据SkeletonCode 生成skeleton_code。当作column name 
