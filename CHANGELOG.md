## [1.2.1](https://github.com/christmas-island/cr-semantic-release/compare/v1.2.0...v1.2.1) (2026-03-15)

### Bug Fixes

* revert template vars — GHA ${{ }} collides with ${} template syntax ([e4a8514](https://github.com/christmas-island/cr-semantic-release/commit/e4a8514405acb48c8dcd5be8df63fa8c67f57384)), closes [common-repo/common-repo#TBD](https://github.com/common-repo/common-repo/issues/TBD)

## [1.2.0](https://github.com/christmas-island/cr-semantic-release/compare/v1.1.0...v1.2.0) (2026-03-15)

### Documentation

* clean up README now that source filtering works on >=0.28.0 ([58003db](https://github.com/christmas-island/cr-semantic-release/commit/58003db568089843a5727a896cbb7b250e0f32ba))

### Features

* templatize GitHub App vars in release workflow ([402ea38](https://github.com/christmas-island/cr-semantic-release/commit/402ea389ee69ad21a40ad1a7d5d144324672fc72))

### Bug Fixes

* template glob should use post-rename path ([6345772](https://github.com/christmas-island/cr-semantic-release/commit/63457723cc0c26fbb1d17c5cf333b68f01ff991f))
* template mark must use pre-rename path, move before rename ([d41cb34](https://github.com/christmas-island/cr-semantic-release/commit/d41cb341b463f24c6fe3891af16fb7354f92a956))

## [1.1.0](https://github.com/christmas-island/cr-semantic-release/compare/v1.0.1...v1.1.0) (2026-03-15)

### Documentation

* update usage for common-repo 0.27.0 workaround ([e99caf6](https://github.com/christmas-island/cr-semantic-release/commit/e99caf614571bb35b4a95c44dcd7f94011074bac)), closes [common-repo/common-repo#229](https://github.com/common-repo/common-repo/issues/229) [#230](https://github.com/christmas-island/cr-semantic-release/issues/230)

### Features

* restore source-declared filtering (requires common-repo >=0.28.0) ([8ba5ad3](https://github.com/christmas-island/cr-semantic-release/commit/8ba5ad3b433fd5edbd13c8c9452f77ea914869bd))

## [1.0.1](https://github.com/christmas-island/cr-semantic-release/compare/v1.0.0...v1.0.1) (2026-03-15)

### Miscellaneous

* add source-level common-repo config ([0f70793](https://github.com/christmas-island/cr-semantic-release/commit/0f70793fe8256fe6f5efd44a5d4e92ce41715643))
* fix source config format ([d911531](https://github.com/christmas-island/cr-semantic-release/commit/d911531f6fb883bccf77c984275dffae28ea4098))
* fix source config to documented format ([ff206f0](https://github.com/christmas-island/cr-semantic-release/commit/ff206f01ee54b0fae959bdd636e81789f72a0e38))
* try exclude instead of include ([22ab420](https://github.com/christmas-island/cr-semantic-release/commit/22ab4208bb2c8afb640fcbe79acc0c3f8efdb7b7))

### Bug Fixes

* remove non-functional source .common-repo.yaml ([9e46120](https://github.com/christmas-island/cr-semantic-release/commit/9e46120f54deea9fe375a6f609e94cef5cf4164a)), closes [common-repo/common-repo#226](https://github.com/common-repo/common-repo/issues/226)

### Code Refactoring

* move distributed files to src/, add sync check CI ([aa94b0a](https://github.com/christmas-island/cr-semantic-release/commit/aa94b0a05736491d5fa3a27f409a7cdb45a73086))
