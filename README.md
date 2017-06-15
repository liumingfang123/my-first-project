# my-first-project
#好吧。开始我的第一个项目
#用mybatise完成对象关系；
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper    
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"    
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace： 对statement进行分类信息管理的 -->
<!-- mapper代理开发方式及其十分重要 -->
<mapper namespace="com.mybatis.OrderMapper">
	<select id="one2one" resultMap="order_map">
		select
		orders.id,
		orders.user_id
		,orders.number,
		user.username,
		user.sex
		from orders,user
		where orders.user_id=user.id
		<!-- select orders.id, orders.number, orders.user_id, user.sex, user.username 
			FROM orders, USER WHERE orders.user_id = user.id -->
	</select>
	<resultMap type="Orders" id="order_map">
		<id column="id" property="id" />
		<result property="user_id" column="user_id" />
		<result property="number" column="number" />
		<association property="user" javaType="User">

			<result property="username" column="username" />
			<result property="sex" column="sex" />
		</association>
	</resultMap>
	<select id="one2one2" resultMap="orders_map">
		select * from orders
	</select>
	<resultMap type="Orders" id="orders_map">
		<id column="id" property="id" />
		<result property="user_id" column="user_id" />
		<result property="number" column="number" />
		<association property="user" javaType="User" column="user_id"
			select="com.mybatis.UserMapper.findUserById"></association>
	</resultMap>
	<select id="one2many" resultMap="order_map1">
		select
		orders.id,
		orders.user_id
		,orders.number,
		user.username,
		user.sex,
		orderdetail.items_id,
		orderdetail.items_num,
		orderdetail.id ideid
		from
		orders,user,orderdetail
		where orders.user_id=user.id
		and
		orderdetail.orders_id=orders.id
	</select>
	<resultMap type="Orders" id="order_map1">
		<id column="id" property="id" />
		<result property="user_id" column="user_id" />
		<result property="number" column="number" />
		<association property="user" javaType="User">
			<result property="username" column="username" />
			<result property="sex" column="sex" />
		</association>
		<collection property="orderdetail" ofType="orderdetail">
			<id column="ideid" property="id" />
			<result property="items_nums" column="items_nums" />
			<result property="items_id" column="items_id" />
		</collection>
	</resultMap>
	<select id="one2many2" resultMap="prder+map">
		select
		orders.id,
		orders.user_id
		,orders.number,
		orderdetail.items_id,
		orderdetail.items_num,
		orderdetail.id ideid
		from orders,orderdetail where orders.id=orderdetail.orders_id
	</select>
	<resultMap type="Orders" id="prder+map">
		<id column="id" property="id" />
		<result property="user_id" column="user_id" />
		<result property="number" column="number" />
		<association property="user" javaType="User" column="user_id"
			select="com.mybatis.UserMapper.findUserById"></association>
		<collection property="orderdetail" ofType="orderdetail">
			<id column="ideid" property="id" />
			<result property="items_num" column="items_num" />
			<result property="items_id" column="items_id" />
		</collection>

	</resultMap>

</mapper>
