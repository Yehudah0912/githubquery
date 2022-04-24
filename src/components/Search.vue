<template>
	<section class="jumbotron">
		<div class="container">
			<h3>Search Github Users</h3>
			<div class="form-inline">
				<input type="text" class="form-control" id="exampleInputAmount" placeholder="Enter the name you search" />
				<button type="submit" class="btn btn-primary">Search</button>
			</div>
		</div>
	</section>
</template>
<script>
export default {
	name: 'Search'
};
</script>
<style lang="less" scoped>
.btn-primary {
	margin-left: 8px;
}
</style>