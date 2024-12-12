<script lang="ts">
	import { onMount } from 'svelte';
	import JSZip from 'jszip';
	let wrapsData: any[] = [];

	onMount(async () => {
		const response = await fetch('/wraps/cybertruck/index.json');
		wrapsData = await response.json();
	});

	function onSubmitDownload(event: Event) {
		event.preventDefault();
		const form = event.target as HTMLFormElement;
		const formData = new FormData(form);
		const selectedWraps = Array.from(formData.keys());
		console.log(selectedWraps);
		// download selected wraps from /wraps/cybertruck/{wrap.path}

		const zip = new JSZip();
		selectedWraps.forEach((wrap) => {
			zip.file(
				wrap,
				fetch(`/wraps/cybertruck/${wrap}`).then((res) => res.blob())
			);
		});

		zip.generateAsync({ type: 'blob' }).then((content) => {
			const url = URL.createObjectURL(content);
			const a = document.createElement('a');
			a.href = url;
			a.download = 'wraps.zip';
			a.click();
		});
	}
</script>

<form on:submit={onSubmitDownload}>
	<div
		class="tds-form-input-group accessories-block-wtih-asset flex h-full w-full flex-row flex-wrap items-center justify-center gap-2"
	>
		{#each wrapsData as authorData}
			{#each authorData.wraps as wrap}
				<div>
					<input
						class="tds-form-input-hidden-choice"
						id={wrap.path}
						type="checkbox"
						name={wrap.path}
					/>
					<label
						class="tds-form-input tds-form-input--option accessories-list-option tds-flex--top tds-flex-item h-full"
						for={wrap.path}
						><span class="tds-form-input-leading"
							><span class="tds-form-input-visual-checkbox"></span></span
						>
						<div
							class="accessories-list-option--label tds-text--contrast-high tds-flex-item tds-flex--justify-center"
						>
							<div class="relative">
								<svg
									version="1.1"
									xmlns="http://www.w3.org/2000/svg"
									class="asset-loader--svg-container asset-loader-2 accessories-asset--container"
									style="overflow: hidden; cursor: inherit; opacity: 1; transform: scale(1);"
								>
									<title>Cybertruck Shell</title>
									<defs></defs>
									<image
										width="100%"
										height="100%"
										xmlns:xlink="http://www.w3.org/1999/xlink"
										xlink:href="/cybertruck-shell.png"
										preserveAspectRatio="xMidYMid "
									>
									</image>
								</svg>
								<!-- <svg
								version="1.1"
								xmlns="http://www.w3.org/2000/svg"
								class="asset-loader--svg-container asset-loader-2 accessories-asset--container absolute left-0 top-0"
								style="overflow: hidden; cursor: inherit; opacity: 1; transform: scale(1);"
							>
								<title>Wrap</title>
								<defs></defs>
								<image
									width="100%"
									height="100%"
									xmlns:xlink="http://www.w3.org/1999/xlink"
									xlink:href="/wraps/cybertruck/{wrap.path}"
									preserveAspectRatio="xMidYMid slice"
								>
								</image>
							</svg> -->

								<img
									class="asset-loader--svg-container asset-loader-2 accessories-asset--container absolute left-0 top-0 max-h-[150px] max-w-[300px]"
									style="{!wrap['dont-crop']
										? 'object-position: bottom; margin-top: -40px; margin-left: 21px; object-fit: cover; width: 92%; height: 92%; clip-path: polygon(39% 51%, 78% 59%, 100% 62%, 100% 100%, 0 100%, 0 86%, 0 67%);'
										: ''} "
									alt="Wrap"
									src="/wraps/cybertruck/{wrap.path}"
								/>
							</div>
							<span
								class="tds-text--contrast-high tds-text--caption tds-text--medium tds-text--center"
							>
								<!-- <svg
								width="24"
								height="24"
								viewBox="0 0 24 24"
								fill="none"
								xmlns="http://www.w3.org/2000/svg"
							>
								<path
									d="M21.9971 18.58V13.09C21.9971 12.9 21.8971 12.63 21.6571 12.54L21.8071 11L21.2671 10.68L21.2971 10.28L21.2871 10.25C21.2271 10.08 19.8771 6.06999 18.7081 4.48999L18.6581 4.42999H6.34206L6.29206 4.48999C5.12206 6.06999 3.77206 10.08 3.71206 10.25L3.70206 10.28L3.73206 10.68L3.19306 11L3.34306 12.54C3.10306 12.63 3.00306 12.9 3.00306 13.09V18.58C2.99306 18.65 2.99306 19.15 3.24306 19.41C3.34306 19.52 3.47306 19.57 3.62306 19.57H5.33306C5.48306 19.57 5.61306 19.52 5.71306 19.41C5.97306 19.15 5.96306 18.65 5.96306 18.58V16.93L6.08306 17.01H18.9181L19.0381 16.93V18.58C19.0381 18.65 19.0281 19.15 19.2881 19.41C19.3881 19.52 19.5181 19.57 19.6681 19.57H21.3781C21.5281 19.57 21.6581 19.52 21.7571 19.41C22.0071 19.15 22.0071 18.65 21.9971 18.58ZM6.52206 4.84999H18.3581C18.3581 4.84999 19.2481 6.76999 19.6781 8.36999H5.33206C5.33206 8.36999 5.91206 6.21999 6.52206 4.84999ZM21.0571 11.06L18.4581 11.71H6.49206L3.94206 11.03L3.90206 10.12L6.58206 10.79H18.4281L21.0981 10.12L21.0581 11.06H21.0571Z"
									fill="currentColor"
								/>
							</svg> -->
								Cybertruck
							</span>
							<span class="tds-text--body tds-text--bold">{wrap.name}</span><span
								class="tds-text--caption flex flex-row"
							>
								by {authorData.author === 'teslamotors' ? 'Tesla' : authorData.author}
								{#if authorData.author === 'teslamotors'}
									<svg
										width="16"
										height="16"
										viewBox="0 0 16 16"
										fill="none"
										xmlns="http://www.w3.org/2000/svg"
										class="ml-1 mt-1.5"
									>
										<path
											d="M8 11C9.65685 11 11 9.65685 11 8C11 6.34315 9.65685 5 8 5C6.34315 5 5 6.34315 5 8C5 9.65685 6.34315 11 8 11Z"
											fill="white"
										/>
										<path
											d="M8 2C7.21207 2 6.43185 2.15519 5.7039 2.45672C4.97595 2.75825 4.31451 3.20021 3.75736 3.75736C3.20021 4.31451 2.75825 4.97595 2.45672 5.7039C2.15519 6.43185 2 7.21207 2 8C2 8.78793 2.15519 9.56815 2.45672 10.2961C2.75825 11.0241 3.20021 11.6855 3.75736 12.2426C4.31451 12.7998 4.97595 13.2417 5.7039 13.5433C6.43185 13.8448 7.21207 14 8 14C9.5913 14 11.1174 13.3679 12.2426 12.2426C13.3679 11.1174 14 9.5913 14 8C14 6.4087 13.3679 4.88258 12.2426 3.75736C11.1174 2.63214 9.5913 2 8 2ZM10.78 7.268L7.905 10.143C7.83557 10.2129 7.753 10.2684 7.66204 10.3062C7.57108 10.3441 7.47352 10.3636 7.375 10.3636C7.27648 10.3636 7.17892 10.3441 7.08796 10.3062C6.997 10.2684 6.91443 10.2129 6.845 10.143L5.22 8.518C5.14834 8.44885 5.09116 8.36612 5.05181 8.27463C5.01246 8.18315 4.99173 8.08474 4.99081 7.98516C4.9899 7.88558 5.00883 7.78681 5.0465 7.69462C5.08417 7.60243 5.13982 7.51866 5.2102 7.44821C5.28059 7.37776 5.3643 7.32203 5.45646 7.28428C5.54861 7.24652 5.64736 7.2275 5.74694 7.22832C5.84653 7.22913 5.94495 7.24978 6.03647 7.28904C6.128 7.3283 6.21078 7.3854 6.28 7.457L7.375 8.552L9.72 6.207C9.78866 6.13331 9.87146 6.07421 9.96346 6.03322C10.0555 5.99223 10.1548 5.97019 10.2555 5.96841C10.3562 5.96663 10.4562 5.98516 10.5496 6.02288C10.643 6.0606 10.7278 6.11674 10.799 6.18796C10.8703 6.25918 10.9264 6.34401 10.9641 6.4374C11.0018 6.53079 11.0204 6.63082 11.0186 6.73152C11.0168 6.83223 10.9948 6.93154 10.9538 7.02354C10.9128 7.11554 10.8537 7.19934 10.78 7.268Z"
											fill="#3E6AE1"
										/>
									</svg>
								{/if}
							</span>
						</div>
					</label>
				</div>
			{/each}
		{/each}
	</div>
	<div class="tds-clip-top-right fixed bottom-0 right-2 h-[65px] w-[320px] rounded-t-xl bg-[#222]">
		<button class="tds-btn tds-btn--primary absolute bottom-2 right-8 max-w-52" type="submit">
			Download
		</button>
		<button class="tds-btn tds-btn--secondary absolute bottom-2 left-4 max-w-40" type="reset">
			Reset
		</button>
	</div>
</form>
