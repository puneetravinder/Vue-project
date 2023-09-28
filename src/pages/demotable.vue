<template>
    <Navbar>
        <template #title>Demo Table</template>
        <template #links>Data table demo</template>
    </Navbar>
    <div class="container is-fluid">
        <table class="table is-hoverable is-fullwidth" style="margin-top: 80px;">
            <thead>
                <tr>
                    <th scope="col" class="is-media"></th>
                    <th scope="col">First Name</th>
                    <th scope="col">Last Name</th>
                    <th scope="col">Position</th>
                    <th scope="col" class="is-end">
                        <div class="dark-inverted is-flex is-justify-content-flex-end">Actions</div>
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td class="is-media">
                        <VAvatar picture="/demo/avatars/8.gif" />
                    </td>
                    <td>Tina</td>
                    <td>Bergmann</td>
                    <td>Head of Sales</td>
                    <td class="is-end">
                        <div class="is-flex is-justify-content-flex-end">
                            <FlexTableDropdown />
                        </div>
                    </td>
                </tr>
                <tr>
                    <td class="is-media">
                        <VAvatar picture="/demo/avatars/1.gif" />
                    </td>
                    <td>John</td>
                    <td>Wistmus</td>
                    <td>Senior Executive</td>
                    <td class="is-end">
                        <div class="is-flex is-justify-content-flex-end">
                            <FlexTableDropdown />
                        </div>
                    </td>
                </tr>
                <tr>
                    <td class="is-media">
                        <VAvatar picture="/demo/avatars/4.gif" />
                    </td>
                    <td>Sam</td>
                    <td>Watson</td>
                    <td>Software Engineer</td>
                    <td class="is-end">
                        <div class="is-flex is-justify-content-flex-end">
                            <FlexTableDropdown />
                        </div>
                    </td>
                </tr>
                <tr>
                    <td class="is-media">
                        <VAvatar initials="JD" color="info" />
                    </td>
                    <td>Jolaine</td>
                    <td>Joestar</td>
                    <td>HR Manager</td>
                    <td class="is-end">
                        <div class="is-flex is-justify-content-flex-end">
                            <FlexTableDropdown />
                        </div>
                    </td>
                </tr>
                <tr>
                    <td class="is-media">
                        <VAvatar picture="/demo/avatars/3.gif" />
                    </td>
                    <td>Anders</td>
                    <td>Jensen</td>
                    <td>Accountant</td>
                    <td class="is-end">
                        <div class="is-flex is-justify-content-flex-end">
                            <FlexTableDropdown />
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
        <!-- <div class="container"> -->
        <VDropdown title="Dropdown with image" spaced>
            <template #content>
                <a href="#" class="dropdown-item is-media">
                    <img class="item-img" src="/images/avatars/svg/vuero-1.svg" alt="" />
                    <div class="meta">
                        <span>Erik K.</span>
                        <span>New York, NY</span>
                    </div>
                </a>
                <a href="#" class="dropdown-item is-media is-active">
                    <img class="item-img" src="/demo/avatars/7.jpg" alt="" />
                    <div class="meta">
                        <span>Alice C.</span>
                        <span>San Diego, CA</span>
                    </div>
                </a>
            </template>
        </VDropdown>
        <VButton color="primary"> Button </VButton>
        <!-- </div> -->
    </div>
</template>