create procedure Main_query
as
begin
	select 
	a.AgentType,
	a.AgentName, 
	a.AgentPhone, 
	a.AgentPriority, 
	a.AgentLogo,
	a.AgentEmail,
	a.AgentAddress,
	a.AgentDirector,
	a.AgentINN,
	a.AgentKPP,
	(case when (select sum(ProductAmount) from AgentProducts s_i
				where s_i.AgentName = a.AgentName) > 0
		  then (select sum(ProductAmount) from AgentProducts s_i
				where s_i.AgentName = a.AgentName)
		  else 0
	 end) as sells,
	(case when ((select sum(p.MinCostForAgent * s_i.ProductAmount)
				from Products p
				Inner Join AgentProducts s_i
				on p.ProductName = s_i.Product
				where s_i.AgentName = a.AgentName) < 10000)
		  then 0
		  when ((select sum(p.MinCostForAgent * s_i.ProductAmount)
				 from Products p
				 Inner Join AgentProducts s_i
				 on p.ProductName = s_i.Product
				 where s_i.AgentName = a.AgentName) < 50000)
		  then 5
		  when ((select sum(p.MinCostForAgent * s_i.ProductAmount)
				 from Products p
				 Inner Join AgentProducts s_i
				 on p.ProductName = s_i.Product
				 where s_i.AgentName = a.AgentName) < 150000)
		  then 10
		  when ((select sum(p.MinCostForAgent * s_i.ProductAmount)
				 from Products p
				 Inner Join AgentProducts s_i
				 on p.ProductName = s_i.Product
				 where s_i.AgentName = a.AgentName) < 500000)
		  then 20
		  when ((select sum(p.MinCostForAgent * s_i.ProductAmount)
				 from Products p
				 Inner Join AgentProducts s_i
				 on p.ProductName = s_i.Product
				 where s_i.AgentName = a.AgentName) > 500000)
		  then 25
		  else 0
	 end) as discount
	from Agents a
	group by a.AgentType, a.AgentName, a.AgentPhone, a.AgentPriority, a.AgentLogo, a.AgentEmail, a.AgentAddress, a.AgentDirector, a.AgentINN, a.AgentKPP
end;
