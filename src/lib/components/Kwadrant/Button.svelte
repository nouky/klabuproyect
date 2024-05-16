<script>
	export let _class;
	export let btnclass;
	export let id;
	export let label;

	btnclass = typeof btnclass !== 'undefined' ? btnclass : 'btn-dark';
</script>

<div class="col row {_class}">
	<button {id} class="btn {btnclass} disabled btn-sheet">
		{label}
	</button>
</div>
