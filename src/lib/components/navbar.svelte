<script lang="ts">
	import { Drawer, drawerStore } from '@skeletonlabs/skeleton';
	import type { DrawerSettings } from '@skeletonlabs/skeleton';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
    import Fa from 'svelte-fa';
    import { faBars, faCircleUser, faMultiply} from '@fortawesome/free-solid-svg-icons';
	import { adminMenu, type TabDefinition } from './navigation.tabs';
	import SettingMenu from './setting.menus.svelte';
	import Tabs from './tabs.svelte';
	let activeTab = '';
	const adminTabs: TabDefinition[] = adminMenu();
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
		const settings: DrawerSettings = { id: 'rightSidebar', position: 'right', width: '900px', bgDrawer: 'bg-primary-50 text-on-primary-token',
			bgBackdrop: 'bg-primary-500/50' };
		drawerStore.open(settings);
	}

    function drawerRightClose(): void {
	drawerStore.close();
}
</script>

<AppShell >
	<svelte:fragment slot="header">
		<AppBar gridColumns="grid-cols-3" background="bg-secondary-500" class="text-white" slotDefault="place-self-center" slotTrail="place-content-end">
			<svelte:fragment slot="lead">
                <div class="">
				<button on:click={drawerLeftOpen}>
               
                 <Fa icon={faBars} size="lg"/>
				</button>
            </div>
            <div>
				<div class="flex-1 justify-start hidden lg:block ml-5">
					<ul class="menu menu-horizontal space-x-4">
					
						{#each adminTabs as t}
						  <a
						  href={t.path}
						  class="hover:bg-[#6c3dc2] hover:text-base-100 px-3 py-2 hover:no-underline rounded-md text-md font-medium {activeTab == t.path
							? 'active: bg-primary-500 text-base-100' : 'text-base-100'}">{t.name}</a>
						{/each}
					  
					</ul>
				  </div>
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
			<!-- <ul class="grid justify-center w-60 mt-5" > -->
				<!-- <button
				>
				<div class="flex  flex-row mt-3 gap-1 ml-3">
					<svg  style="color: rgb(242, 75, 33);" xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mt-1 feather feather-log-out"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4" fill="#f24b21"></path><polyline points="16 17 21 12 16 7"></polyline><line x1="21" y1="12" x2="9" y2="12"></line></svg>
					 <span class="text-[12px] mt-1" style="color: rgb(242, 75, 33);">Sign Out</span>
				  </div>
				  </button>
			   
				 <button style="color: rgb(242, 75, 33);" class='close absolute top-2 right-3' on:click={drawerRightClose}><Fa icon={faMultiply} size="19" class=" ml-2 mt-2" /></button> -->
				<SettingMenu on:click = {drawerRightClose}/>
                <!-- <button on:click={drawerRightClose}></button> -->
            <!-- </ul> -->
		{:else if $drawerStore.id === 'leftSidebar'}
			<ul class="grid justify-center w-60 mt-5">
				{#each adminTabs as t}
				<a
				href={t.path}
				class="hover:bg-[#6c3dc2] hover:text-base-100 px-3 py-2 hover:no-underline no-underline rounded-md text-md font-medium {activeTab == t.path
				  ? 'active: bg-primary-500 text-base-100' : 'text-base-100'}">{t.name}</a>
			  {/each}
			</ul>
		{:else}
			<p>(fallback contents)</p>
		{/if}
	</Drawer>
</div>
