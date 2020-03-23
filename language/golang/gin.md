Gin 中对与时间戳的处理，　有一定的问题 
 
```golang
type BasicPackageInfoQuery struct { 
    // OriginStore 数据磁盘ID 
    DiskID string `json:"disk_id,omitempty" form:"origin_store"` 
    // CapturedBy 拍摄的设备 
    CapturedBy string `json:"captured_by,omitempty" form:"captured_by"` 
    ShootStartTime time.Time `json:"shoot_start_time,omitempty" form:"shoot_start_time" time_format:"2006-01-02T15:04:05Z"` 
    ShootEndTime time.Time `json:"shoot_end_time,omitempty" form:"shoot_end_time"` 
    UpdateStartTime time.Time `json:"update_start_time,omitempty" form:"update_start_time"` 
    UpdateEndTime time.Time `json:"update_end_time,omitempty" form:"update_end_time"` 
    Status *int `json:"status,omitempty" form:"status"` 
    PackageType *int `json:"package_type,omitempty" form:"package_type"` 
} 
```
如图所示，使用shouldBindQuery进行绑定的时候，只有ShootStartTime可以被成功绑定，其他的时间会报time blank format 
 
输入的时间格式　2006-01-02T15:04:05 
 
但是对于shouldBind来绑定req 的data信息则可以不用指定time_stamp 
 
 
三种可以解析的格式 
2002-10-02T15:00:00+00:00 
 
 
2002-10-02T15:00:00Z 
 
 
2002-10-02T15:00:00.05Z 
