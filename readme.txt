更新记录

0.0.4
支持类表自动扩展字段（新的字段只能增加，不能删除或是修改类型）
支持更新数据时，是否替换Nil字段为默认值（insert插入数据时，过滤掉为nil字段的值）

0.0.3
支持在类中添加unionPrimaryKeys作为联合关键字【关键字定义类型只支持基本类型NSNumber，NSString】

0.0.2
支持NSArray：如果是自定义类，需要实现encodeWithCoder和initWithDecoder；(详见测试用例）

0.0.1
直接保存类到数据库中
支持类型：NSString、NSNumber、NSData；
支持类嵌套：类中再定义子类；
支持数据库加密处理：可按类定义不同的加密密钥；【需要添加FMDB/SQLCiper第三方库】
支持数据库按版本自动迁移；

说明
/*

//数据模型:
1,+VERSION：数据库版本，不同的版本会对数据库进行自动升级；
2,+PASSWORD：单独设置数据库密码（此密码为最优先级，依次为Mgr设置的Class密码->通用密码）
3,_id：该字段为数据库内置关键字，readonly[自增]

@interface EDBTestModel : NSObject

@property (nonatomic, readonly) NSString *_id; //default primary key

+ (NSString *)VERSION;
+ (NSString *)PASSWORD; //该密码为最优先级

@end

@implementation EDBTestModel

+ (NSString *)VERSION{
return @"1.1";
}

+ (NSString *)PASSWORD{
return @"123456";
}

@end


//TODOList
1，模型支持关键字，insert时，使用关键字做区分，避免重复插入

最初版本源代码来源于该项目：
https://github.com/netyouli/WHC_ModelSqliteKit
