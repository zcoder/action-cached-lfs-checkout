# GitHub action: Cached LFS checkout

Storing (large) binary files in Git trees is not recommended because any change to the
file will result in a re-upload of the entire file when pushing, increasing the size of
the Git repository. When updating a 100 MB file 100 times, your repository will be 10 GB
in size!

As a remedy, there is [Git LFS](https://git-lfs.github.com/) which stores certain files
only as pointers in the Git tree, downloading the actual data from somewhere else when
pulling. The repository size remains small.

[GitHub applies some fees when the total amount of LFS downloads surpasses
1GB.](https://github.com/github/roadmap/issues/237) Unfortunately, even gh-actions runs,
when used with

```yaml
- name: Checkout code
  uses: actions/checkout@v4
  with:
    lfs: true
```

count towards that limit. To _cache_ the LFS downloads, you can instead use this action.
Simply replace the above by

```yaml
- name: Checkout code
  uses: zcoder/action-cached-lfs-checkout@v5
  # Use these to explicitly include/exclude files:
  # with:
  #   include: "*"
  #   exclude: ""
```

Check it out [on the GitHub
Marketplace](https://github.com/marketplace/actions/cached-lfs-checkout)!

### Further reading

- [Luca Benci, Avoiding git-lfs bandwidth waste with GitHub and
  CircleCI](https://www.develer.com/en/avoiding-git-lfs-bandwidth-waste-with-github-and-circleci/)
- [actions/checkout issue: Cache for
  LFS](https://github.com/actions/checkout/issues/165)

### License

The scripts and documentation in this project are released under the MIT License.
