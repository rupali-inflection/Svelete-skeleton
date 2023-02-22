<script lang="ts">
	import { Drawer, drawerStore } from '@skeletonlabs/skeleton';
	import type { DrawerSettings } from '@skeletonlabs/skeleton';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
    import Fa from 'svelte-fa';
    import { faBars, faCircleUser } from '@fortawesome/free-solid-svg-icons';
	import SettingMenu from './setting.menus.svelte';
	import Tabs from './tabs.svelte';

	function drawerLeftOpen(): void {
		const settings: DrawerSettings = {
			id: 'leftSidebar',
			position: 'left',
			width: '800px',
			bgDrawer: 'bg-primary-50 text-on-primary-token',
			bgBackdrop: 'bg-primary-500/50'
		};
		drawerStore.open(settings);
	}

	function drawerRightOpen(): void {
		const settings: DrawerSettings = { id: 'rightSidebar', position: 'right', width: '800px' };
		drawerStore.open(settings);
	}

    function drawerRightClose(): void {
	drawerStore.close();
}
</script>

<AppShell >
	<svelte:fragment slot="header">
		<AppBar gridColumns="grid-cols-3" background="bg-primary-500" class="text-white" slotDefault="place-self-center" slotTrail="place-content-end">
			<svelte:fragment slot="lead">
                <div class="lg:hidden">
				<button on:click={drawerLeftOpen}>
               
                 <Fa icon={faBars} size="lg"/>
				</button>
            </div>
            <div>
                <Tabs />
            </div>
			</svelte:fragment>
            <div>
                <img class="block h-8 w-8 " src="/rean-logo-white.png" alt="REAN" />
              </div>
			<svelte:fragment slot="trail">
				<button on:click={drawerRightOpen}>
					<Fa icon={faCircleUser} size="lg" />
				</button>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<slot />
	<svelte:fragment slot="footer">
			<footer class="text-center w-full fixed bottom-0 h-11 bg-primary-500">
				<a href="https://reanfoundation.org">
					<p
						class="mt-3 text-white text-sm hover:underline-offset-3 hover:underline decoration-indigo-500"
					>
						&#xa9; 2022 REAN Foundation
					</p></a
				>
			</footer>
		</svelte:fragment>
</AppShell>
<div class="w-[60%]">
	<Drawer>
		{#if $drawerStore.id === 'rightSidebar'}
			<ul class="grid justify-center w-60 mt-5" >
				<!-- <SettingMenu/> -->
                <!-- <button on:click={drawerRightClose}></button> -->
            </ul>
		{:else if $drawerStore.id === 'leftSidebar'}
			<ul class="grid justify-center w-60 mt-5">
				<li class=" mt-4 text-xl hover:bg-primary-500">
					<a href="/home" class="no-underline"> Dashboard </a>
				</li>
				<li class=" mt-4 text-xl hover:bg-primary-500">
					<a href="/" class="no-underline"> About Us </a>
				</li>
				<li class="relative mt-4 text-xl hover:bg-primary-500">
					<a href="/" class="no-underline"> Contact </a>
				</li>
				<li class="relative mt-4 text-xl hover:bg-primary-500">
					<a href="/" class="no-underline"> Help </a>
				</li>
			</ul>
		{:else}
			<p>(fallback contents)</p>
		{/if}
	</Drawer>
</div>
